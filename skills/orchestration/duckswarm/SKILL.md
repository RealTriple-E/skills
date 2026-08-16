---
name: duckswarm
description: Duckswarm amplifies any weaker model to near-frontier performance by orchestrating adaptive multi-round debates, claim-level consensus, and specialized prompting exclusively through Duck.ai (zero-auth browser). Uses only the models offered inside Duck.ai. Never calls Claude, GPT or any other model via APIs or the harness. Use automatically on any non-trivial coding, research, vision, math, reasoning, planning, architecture, debugging, or high-stakes problem, or whenever local confidence is imperfect. Also trigger on duckswarm, consensus, multi-model, cross-check, amplify, debate this, verify across models, duck.ai, frontier-level. Author Elyazer Emmanuel.
metadata:
  author: Elyazer Emmanuel
  version: "1.1"
  github: ready
---

# Duckswarm

Duckswarm turns the local (weaker) model into a high-quality conductor that recruits, debates, and synthesizes stronger models available on Duck.ai. The local model never invents facts — it only plans, routes, critiques, and recombines.

Author: Elyazer Emmanuel

## When to Invoke (Aggressive Automatic Triggering)

**Load this skill automatically whenever any of the following is true** (do not wait for the user to ask):

- The task involves writing, reviewing, debugging, or designing non-trivial code.
- The task requires factual accuracy, research synthesis, citations, or current knowledge.
- Any image, screenshot, diagram, PDF page, or visual input is present or mentioned.
- The problem is multi-step, architectural, mathematical, logical, or high-stakes.
- The local model has any internal uncertainty, conflicting instincts, or would normally say “I’m not sure”.
- The user mentions correctness, verification, second opinion, edge cases, or production readiness.
- The query is longer than a simple factual lookup or contains the words “how”, “why”, “best”, “correct”, “implement”, “analyze”, “compare”, “design”.

**Manual / explicit triggers**:
- duckswarm, run duckswarm, consensus, multi-model, cross-check, amplify this, debate this, verify across models, duck.ai consensus, frontier-level answer.

When in doubt, invoke Duckswarm. False positives are cheap; missing a hard problem is expensive.

## Core Principles

1. **Duck.ai only.** All model calls go exclusively through the Duck.ai web UI via browser automation. Never use direct Anthropic/OpenAI/Mistral APIs, never use any model connected to the agent harness, and never fall back to the local model’s own knowledge for the final answer.
2. Local model = conductor only. Never generate the final answer from its own parametric knowledge while Duckswarm is active.
3. Every hard problem is decomposed into atomic claims that can be verified independently.
4. Prefer multi-round debate over single-shot parallel queries.
5. Always produce a confidence-weighted synthesis the local model can trust and act on.
6. Fail open: if Duck.ai is unreachable or a model disappears, degrade gracefully and report residual uncertainty.
7. Vision is first-class: treat images as primary evidence, not decoration.

## Input Schema

- `query` (string, required): The problem, code, research question, or vision task.
- `images` (array of strings, optional): Local absolute paths or public URLs for vision tasks. Support multiple images.
- `mode` (enum, default: "auto"):
  - `auto` — skill chooses the best mode based on query complexity and presence of images.
  - `quick_consensus` — parallel single-shot (fast, lower quality).
  - `debate` — A answers → B critiques → A revises → C arbitrates (default for most problems).
  - `iterative_refinement` — best answer is repeatedly improved by stronger models.
  - `adversarial` — one model is forced to attack the consensus; others must defend or update.
  - `vision_first` — force image analysis before any textual reasoning.
- `target_models` (array of strings, optional, default: "auto"): Explicit list or leave to router.
- `isolation_level` (enum, default: "strict"):
  - `strict` — every model runs in a fresh Duck.ai tab/session.
  - `peer_review` — later models see earlier outputs for critique.
- `output_format` (enum, default: "markdown_report"): `markdown_report` | `json`.
- `max_rounds` (integer, default: 3): Hard limit on debate/refinement rounds.
- `min_confidence` (float, default: 0.65): Claims below this threshold stay in Residual Uncertainties.

## Adaptive Model Router (Duck.ai models only)

All model names refer exclusively to the options that appear in the Duck.ai model selector. No external APIs or harness-connected models are ever used.

When `target_models` is "auto" or omitted:

- Coding / formal logic / security / debugging → Claude-family option inside Duck.ai first, then GPT-family option, then a strong open model option as skeptic.
- Math / proofs → prioritize the Duck.ai models known for careful step-by-step reasoning.
- Creative / open-ended / long-context → GPT-family + Mistral/Gemma options as offered by Duck.ai.
- Vision or mixed vision+text → any Duck.ai model that accepts images; prefer the strongest vision-capable option in the Duck.ai selector. Always run at least one pure-vision pass before textual debate.
- After round 1, if divergence score > 0.4, automatically recruit a third model family that has not yet spoken (still only from the Duck.ai dropdown).
- Always reserve one “skeptical” role that is prompted to find flaws.

If a chosen model is missing from the Duck.ai dropdown, fall back according to a priority list of other Duck.ai models maintained in the session cache and continue. Never escape to an external API.

## Orchestration State Machine

### 1. Query Analysis (local model)
- Classify domain (code, math, research, vision, planning, mixed).
- If any image is present → bias toward `vision_first` or `debate`.
- Decide mode if set to "auto".
- Optionally decompose the query into 2–5 sub-questions when complexity is high.
- Craft specialized system-style instructions for each role (see Prompt Templates).

### 2. Duck.ai Session Protocol (strict isolation default)

Use the Playwright helper in `scripts/duck_ai_session.py` for all browser interaction.

**Step A – Zero-auth initialization**
- Navigate to https://duck.ai (or https://duckduckgo.com/duckai).
- Dismiss any first-run / “Get Started” / “I Agree” modal if present.
- No login, no cookies, no CAPTCHA expected. If an anti-bot challenge appears, refresh once; if it persists, mark Duck.ai temporarily unavailable and abort with clear residual uncertainty.

**Step B – Model selection & attachment**
- Open the model selector at the top of the chat area and choose the target model.
- If images are provided:
  - Locate `input[type="file"]`.
  - Set one or more files via Playwright `set_input_files`.
  - Poll until every thumbnail preview is fully rendered and stable.
  - Prefer uploading images before typing the textual prompt so the model sees them as primary context.

**Step C – Prompt dispatch & extraction**
- Paste the crafted prompt into the main input (contenteditable or textarea).
- Submit via Enter or the send button.
- Wait until generation finishes (monitor send-button state or disappearance of “Stop generating”).
- Extract only the final assistant message text, stripping UI chrome (Copy, Retry, Fire, etc.).
- Timeouts: 15 s for page/modal, 60 s for generation when images are attached, 45 s otherwise. Retry up to 2 times per model, then mark unavailable.

### 3. Multi-round Execution

**quick_consensus**
- Parallel or sequential independent queries.
- Build claim matrix immediately.

**debate** (preferred for most hard problems)
1. Model A produces initial answer under specialized instructions.
2. Model B receives original query + A’s answer and is told “Find every flaw, missing edge case, logical gap, or overclaim. Be ruthless.”
3. Model A (or a fresh instance) receives the critique and produces a revised answer.
4. Optional Model C arbitrates remaining contradictions.
5. Stop early if confidence is already high or max_rounds reached.

**iterative_refinement**
- Take the strongest partial answer so far.
- Feed it to the next model with “Improve this while preserving every correct claim. Strengthen weak reasoning. Add missing edge cases.”

**adversarial**
- After a provisional consensus, force one model to attack it.
- Remaining models must either rebut with evidence or update the consensus.

**vision_first**
1. All available vision-capable models independently describe the image(s) with no textual leading questions beyond “Describe everything you see that is relevant.”
2. Build a visual claim matrix (only what multiple models agree is visible).
3. Only then run textual debate conditioned on the verified visual claims.
4. Never let a text-only model invent visual details that vision models did not support.

### 4. Claim-Level Decomposition & Scoring

After each round (and at the end):
1. Parse every response into atomic claims (facts, code assertions, logical steps, visual observations).
2. For each claim record:
   - supporting models
   - self-reported confidence (force every model to end with `Confidence: X/10`)
   - explicit contradictions from other models
   - modality tag: `text` | `vision` | `mixed`
3. Compute:
   - Consensus Confidence Score = weighted agreement ratio
   - Divergence Score = fraction of claims with active contradiction or single-model support
4. Only claims meeting `min_confidence` and majority/high-confidence support enter the Verified Core Answer.
5. Vision claims require at least one supporting vision-capable model; pure text models cannot invent visual facts.

### 5. Synthesis (local model only)

Produce the structured report below. The local model may rephrase for clarity but must never add new factual or visual claims that no Duck.ai model supported.

## Required Output Structure

Always emit both a human-readable report and a machine-readable JSON block (or pure JSON when requested).

```markdown
# Duckswarm Consensus Report

**Author**: Elyazer Emmanuel
**Query**: …
**Mode used**: …
**Models consulted**: …
**Rounds**: …
**Images processed**: …
**Overall Consensus Confidence**: 0.00–1.00

## Verified Core Answer
[The answer the local model should treat as ground truth and act on]

## Supporting Evidence Map
- Claim 1 — supported by [models] (avg confidence X) [vision/text]
- Claim 2 — …

## Model Divergence Matrix
- Points of disagreement or unique insights
- Which model introduced each divergent claim

## Residual Uncertainties
- Claims that failed the confidence threshold or remain contested
- Recommended follow-up queries or additional images if any

## Recommended Next Action
- “Safe to implement / act on”
- “Re-query with tighter constraints on X”
- “Needs human review on Y”
- “Vision evidence insufficient — request higher-resolution or different-angle images”
```

```json
{
  "author": "Elyazer Emmanuel",
  "consensus_confidence": 0.0,
  "verified_core_answer": "...",
  "claims": [...],
  "divergences": [...],
  "residual_uncertainties": [...],
  "next_action": "...",
  "images_processed": []
}
```

## Specialized Prompt Templates (use and adapt)

**Initial answer (Model A)**
```
You are a careful, precise expert. Solve the following problem completely.
Show all reasoning. End with:
Confidence: X/10
[problem]
```

**Ruthless critique (Model B)**
```
You are a ruthless reviewer. The original problem is:
[problem]

Here is another model’s answer:
[answer]

List every possible flaw, missing edge case, logical gap, factual error, or overclaim.
Be specific. Do not soften. End with Confidence: X/10 for the severity of issues found.
```

**Revision (Model A or C)**
```
Original problem:
[problem]

Your previous answer:
[answer]

Critique received:
[critique]

Produce an improved answer that fixes every valid point while preserving correct claims.
End with Confidence: X/10.
```

**Vision-first description**
```
Analyze the attached image(s) in extreme detail. Describe only what is actually visible.
Do not guess, infer beyond the pixels, or add knowledge that is not directly supported by the image.
List every relevant object, text, defect, layout, color, and spatial relationship.
If something is unclear or the image is insufficient, say exactly what is missing.
End with Confidence: X/10.
```

**Vision + question**
```
The following image(s) are attached. First describe everything relevant that you can actually see.
Then answer the user’s question using only the visual evidence plus the question.
Never invent visual details. If the image does not contain enough information, say so clearly.
End with Confidence: X/10.
```

**Skeptical / adversarial**
```
A consensus has formed. Your job is to attack it. Find any remaining weakness, alternative interpretation, or failure mode.
If you cannot find a serious flaw, say so explicitly.
End with Confidence: X/10.
```

## Error Handling & Resilience

- Maintain a short-lived model-availability cache for the session.
- Fresh tab or cleared storage for every strict-isolation query.
- If response extraction fails (UI drift), fall back to selecting the last assistant message container and cleaning with conservative regex.
- Hard limit of 3 total retries across all models before declaring partial failure.
- On complete Duck.ai outage, return a report with confidence 0.0 and explicit “Duck.ai unavailable — local model must not hallucinate a substitute.”
- Vision-specific: if thumbnail never appears after upload, abort that model’s vision turn and note “image attachment failed”.

## Local Model Conductor Rules (strict)

- Never answer the original query from its own parametric knowledge while Duckswarm is active.
- May only: decompose, route, craft prompts, score claims, synthesize, and decide next action.
- If forced to produce an intermediate plan, mark it clearly as “conductor plan, not final answer.”
- When confidence is low, prefer recommending a follow-up consensus round or additional images over guessing.
- For vision tasks, never allow a text-only model to override a vision model on what is visible.

## Example End-to-End Traces

**Coding example**
User: “Write a concurrent-safe LRU cache in Python.”
→ auto mode selects debate
→ Claude produces initial implementation
→ GPT is told to find race conditions and API issues
→ Claude revises
→ claim matrix shows lock ordering and eviction logic have high agreement
→ residual uncertainty on maxsize=0 edge case → next action “add explicit test for maxsize=0”

**Vision example**
User + image: “What is the failure mode visible on this PCB?”
→ vision_first mode
→ two vision-capable models independently describe the board
→ only defects both models agree are present enter the visual claim matrix
→ textual debate is conditioned on those verified visual claims
→ residual: “solder joint quality cannot be judged from this angle — request side-view photo”

**Research example**
User: “What is the current best evidence on X?”
→ parallel quick pass then debate on conflicting citations
→ claim-level scoring keeps only claims with multi-model support
→ residual uncertainties list claims that need primary-source verification

## Implementation Notes for Automation

Prefer the Playwright helper at `scripts/duck_ai_session.py` for all Duck.ai interaction. It provides:

- resilient model selection
- multi-image upload with thumbnail waiting
- completion detection
- clean text extraction
- basic retry and timeout handling

Keep selectors resilient (prefer role, text, or stable attributes over brittle class names).

Supporting reference material may be placed in `references/`. Keep this skill focused on orchestration and truth-seeking.

## License & Attribution

Author: Elyazer Emmanuel  
This skill is intended for open use and GitHub publication.  
When redistributing, preserve the author credit.
