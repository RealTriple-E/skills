# Security Architecture — Persistent Browser Session

Author: Elyazer Emmanuel  
Applies to: X Growth Intelligence Skill v1+

## Threat Model Summary

Critical risks: session credential exfiltration, session replay/hijacking, prompt-injection leading to credential leak, over-privileged browser context, behavioral detection leading to account restriction, residual plaintext data on disk.

## Persistent Session Design (CAPTCHA-aware)

Because fresh login on every run triggers repeated CAPTCHA / “prove you are not a robot” challenges, the skill uses a **persistent encrypted browser storage state**.

### Rules

1. Storage state (cookies + localStorage + sessionStorage) is kept persistent across runs.
2. It is encrypted at rest using an OS keychain, age, sops, or the agent’s native secret store.
3. The storage location is **outside** the skill directory tree, outside any agent working directory that could be committed, and outside shared memory that other roles can read.
4. Only the **Publisher** role may load or refresh the session. Scout, Writer, Reviewer and Analyst never receive it.
5. On authentication failure, unexpected logout, unsolvable CAPTCHA, or soft-block:
   - Discard or mark the current state invalid.
   - Block the associated Kanban task with reason `re-auth-required`.
   - Surface a clear human message requesting interactive re-login.
   - Never attempt automated CAPTCHA solving inside the skill.
6. After human completes a fresh login in a controlled browser, the new storage state is re-encrypted and stored. Subsequent runs resume.
7. On skill uninstall or explicit “forget account”, securely delete the storage state and any associated profile directory.
8. Never log, print, echo, or place session material (cookie values, storage-state blobs, tokens, CSRF values) into prompts, conversation history, debug output, dry-run reports, or git.

## Browser Context Hardening

- Dedicated profile directory (persistent but locked down).
- Disable unnecessary permissions (geolocation, notifications, camera, microphone).
- Prefer realistic user-agent, viewport, locale and timezone consistent with the Account Profile’s Geographic Intelligence.
- Network allow-list restricted to x.com / twitter.com domains when the runtime supports it.
- No persistent service workers or background sync beyond what the real UI requires.

## Logging Boundaries

**Allowed:** action type, public post ID, timestamp, success/failure, quality-gate scores, Kanban task ID, high-level error class (e.g. “auth-challenged”).

**Forbidden:** any cookie value, full storage-state, Authorization headers, CSRF tokens, full request/response bodies containing session material.

## Rate & Behavioral Discipline (security-relevant)

- Hard daily action caps well below automation thresholds.
- Irregular inter-action delays with human-like jitter.
- No rapid successive actions or identical repetitive replies.
- Circuit-breaker: any “try again later”, CAPTCHA, or soft-block immediately stops further actions and surfaces for human review.

## Skill-Level Declarations

- The skill requests no more filesystem or network access than each engine strictly needs.
- SKILL.md and all reference files contain zero credentials or session material.
- The skill refuses to operate if a user attempts to supply raw cookies or storage state inside a prompt.
- Independent security scanning of the published skill (and resulting score) should be recorded in README.md and SECURITY.md once available.

## Separation of Concerns

Intelligence layers (Objective, Audience, Trend, Writing, Guardrails, Quality Gates) never receive the session.  
Only the thin Publisher adapter loads it at the moment of execution.  
This keeps the blast radius minimal if any other agent role is compromised.

## Recovery Path

```
Session load or action fails with auth challenge
  → mark state invalid
  → Kanban task → blocked (re-auth-required)
  → notify human
  → wait for new encrypted storage state
  → never fall back to any alternative or cached credential
```
