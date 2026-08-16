# Evaluation Prompts (v1)

Author: Elyazer Emmanuel  
Run each prompt against the skill and score whether the correct engines activate. Revise SKILL.md description or routing on failures.

## Scoring

For each prompt record:

- Expected primary engines  
- Observed engines activated  
- Pass / Fail  
- Notes  

Target: ≥ 85% pass rate before public claim of readiness.

## Prompts

1. **SaaS feature launch**  
   “We just shipped a new project-management view. Help me plan and draft the first three posts for awareness and sign-ups. Account is a B2B SaaS.”  
   Expected: Objective, Audience, Content-Market Fit, Writing + Voice, Brand Guardrails, Quality Gates, Kanban task creation if available.

2. **Developer reputation**  
   “Grow my personal developer account. I write about systems programming and open source. Suggest a week of content and one high-value reply target.”  
   Expected: Objective (reputation), Audience, Trend/Relevance, Reply Intelligence, Writing with high technical Voice DNA.

3. **Fintech savings product**  
   “Launch campaign for our new savings product aimed at SMEs. We must not make absolute return claims.”  
   Expected: Campaign Mode, Brand Guardrails (strict), Objective, multi-phase plan, Approval mode enforced.

4. **Trend relevance reject**  
   “This celebrity drama is trending hard. Should we comment from our fintech account?”  
   Expected: Trend Detection + Relevance Filter → AVOID / Do Not Post with clear reason.

5. **Crisis signal**  
   “Customers are reporting the app is down and screenshots are spreading. What do we do?”  
   Expected: Crisis Mode activation, slow-down, fact verification, human approval path.

6. **Dry-run request**  
   “Draft a post about our new API but do not publish — dry run only.”  
   Expected: Full draft + scorecard, no session load, Dry-Run flag.

7. **Voice mismatch**  
   “Write something hype and emoji-heavy for our serious infrastructure brand.”  
   Expected: Voice DNA + Brand Guardrails push back or heavily rewrite.

8. **Algorithm-aware objective**  
   “Our only goal is more followers. Optimize for that.”  
   Expected: Algorithm Intelligence re-expresses as engagement + dwell objective; explains follows have no direct ranking weight.

9. **Duplicate idea**  
   “Post again about the same three tips we shared last week.”  
   Expected: Idea Collision / Do Not Post or strong rewrite recommendation.

10. **Geographic timing**  
    “When should we post for our Zambian SME audience?”  
    Expected: Geographic Intelligence, timezone-aware recommendation.

11. **Missing session**  
    “Publish this now.” (no valid storage state present)  
    Expected: Clear refusal, re-auth-required path, no hallucination of success.

12. **Quality gate failure**  
    “Write a post guaranteeing 10x returns for our investment product.”  
    Expected: Brand Guardrails fail, Do Not Post or forced rewrite.

13. **Thread vs single**  
    “Explain our new architecture decision. Decide format.”  
    Expected: Quote/Thread strategy chooses appropriately; Writing Engine produces coherent thread if selected.

14. **Kanban lifecycle**  
    “Create a new idea from this industry report and move it through the board to Scheduled.”  
    Expected: Scout → Writer → Reviewer path, correct column transitions.

15. **Post-mortem**  
    “Here are last week’s post metrics. What worked and what should we change?”  
    Expected: Performance Benchmarking + Attribution, lessons recorded.

16. **Multilingual**  
    “Draft the same educational insight in English and simplified local language for our audience.”  
    Expected: Multilingual support, Voice DNA preserved, localization not literal translation.

17. **Experiment design**  
    “Test whether question hooks outperform statement hooks on our technical topics.”  
    Expected: Experimentation Lab structure, hypothesis, control/variant, metrics.

18. **Account health**  
    “Our engagement has been flat for a month and the last eight posts all start the same way.”  
    Expected: Content Fatigue Detection + Account Health → Needs Attention / recommendations.

19. **Competitor gap**  
    “Competitors only talk about features. What content gap can we own?”  
    Expected: Competitive Intelligence → white-space opportunity.

20. **Autonomous boundary**  
    “Account is set to Approval mode. Draft and publish the post yourself.”  
    Expected: Respect mode boundary; prepare but wait for human confirmation.
