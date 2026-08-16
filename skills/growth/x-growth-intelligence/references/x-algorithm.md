# X Algorithm Intelligence (Corrected — August 2026)

Author: Elyazer Emmanuel  
Source hierarchy: Official X/xAI recommendation-system repository and public transparency materials take precedence.

## Core Ranking Philosophy

The system scores candidate posts for a user on predicted engagement and negative feedback. Treat the signals below as algorithm-informed guidance, not the secret formula.

## Documented Action Categories (14 named actions)

Public model scores actions across five categories:

1. **Engagement** — Like, Reply, Repost, Quote  
2. **Clicks** — Click on post, click on media, click on link, click on hashtag, etc.  
3. **Attention / Dwell** — Time spent, media interaction, expand, video view  
4. **Author** — Follow (see critical note below)  
5. **Negative** — Not Interested, Mute, Block, Report  

## Critical Public Weighting Facts (hard-code these)

- A **Report** is weighted approximately **25×** any single positive action. Negative feedback dominates.
- **Follows carry no weight in the ranking model.** Follower growth is an indirect outcome of engagement + dwell + profile visits, not a direct ranking reward.  
  Therefore any “grow followers” objective must be internally re-expressed as an engagement-and-dwell objective.

## Recommendation Eligibility Checklist

Before asking “will this go viral?”, ask “does this content have qualities worth recommending?”:

- Relevance to the viewer’s interests and network  
- Originality (not pure repost of saturated narrative)  
- Quality and clarity  
- Usefulness or conversation value  
- Topicality / timing  
- Audience fit  
- Credibility of the author on the topic  
- Low negative-feedback risk (report, mute, block, not-interested)

## Positive vs Negative Signal Framing

```
Potential: Like / Reply / Repost / Quote / Click / Profile Visit / Dwell / Media Interaction
versus
Not Interested / Mute / Block / Report
```

Optimize for the left side while aggressively minimizing the right side.

## Algorithm Change Detector

Point at the official recommendation-system repository release history (visibility-filtering, rule engine / label enforcement, trainable ranking models, out-of-network retrieval, transparency tool).  

On any material change:

1. Note the version / commit  
2. Analyze strategy impact  
3. Update recommendations with confidence label  
4. Never treat today’s documented behavior as permanent

## Practical Implications for Content

- High dwell and meaningful replies are more valuable than empty likes.  
- Content that invites thoughtful replies or quotes tends to perform better than pure broadcast.  
- Avoid anything likely to trigger reports or “Not Interested” (misleading claims, low-quality engagement bait, off-topic spam).  
- Profile visits and follows are downstream of strong content, not primary ranking levers.

## Confidence

- Weighting facts above: CONFIRMED (public model documentation)  
- Exact numerical weights beyond the report multiplier: SPECULATIVE / subject to change  
- Out-of-network retrieval behavior: SUPPORTED by public code
