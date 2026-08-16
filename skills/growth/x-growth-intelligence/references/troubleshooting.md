# Troubleshooting

Author: Elyazer Emmanuel

## Session / Auth Issues

| Symptom | Action |
|---------|--------|
| CAPTCHA or login wall | Block Kanban task `re-auth-required`, surface to human, wait for new encrypted storage state |
| Soft-block / “try again later” | Circuit-breaker: stop further actions, block task, notify human |
| Session loads but actions fail silently | Treat as invalid; force re-auth path |
| Publisher cannot find storage state | Refuse to publish; report missing session clearly |

## Content Quality

| Symptom | Action |
|---------|--------|
| Repeated AI patterns | Re-run Human Writing Engine; strengthen Voice DNA examples |
| Brand guardrail violation | Fail gate; rewrite or block |
| Weak hook or low conversation potential | Return to Content-Market Fit; consider different angle or “Do Not Post” |
| Duplicate of recent content | Idea Collision → Rewrite / Merge / Save for later |

## Kanban / Lifecycle

| Symptom | Action |
|---------|--------|
| Task stuck in Scheduled | Check heartbeat; reclaim if Publisher process died |
| Reviewer and human disagree | Human decision wins; record reason in comment |
| Campaign phase blocked | Verify linked predecessor has reached Published |

## General

- Missing capability (search, publish, analytics) → say so plainly; never hallucinate success.
- Dry-run always available and preferred for testing.
- When in doubt about risk, default to “Do Not Post” or Approval mode.
