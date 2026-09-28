---
name: social-trend-scout
description: >-
  Monitors TikTok and Instagram for trending content that fits your brand's
  niches, writes a one-line creative angle for each, and posts a curated digest
  to your team's idea channel. Flags every audio trend with a commercial
  clearance warning. Trigger: run the trend scout, pull this week's trends,
  what's trending for us.
---

# Social Trend Scout

Finds rising TikTok and Instagram trends (audio, copy formats, concepts, visuals) filtered for your niches, labels each one, and writes how your brand could adapt it. Audio trends always carry a clearance warning.

## Setup

```
[FILL IN]
BRAND_NAME       = [your brand]
BRAND_FIT        = [what's on-brand, e.g. "playful, colorful, fashion-forward"]
OFF_LIMITS       = [what to skip, e.g. "dark humor, political, anything crude"]
NICHES           = [your content niches, e.g. "your category, pop culture, relatable humor, broadly adaptable"]
FORMAT_LABELS    = [Trending Audio, Trending Copy Format, Trending Concept / Visual]
POST_DESTINATION = [chat channel for ideas]
STATE_FILE       = posted-trends.json   (next to this SKILL.md, starts as [])
LOOKBACK         = [e.g. past 3 days]
MIN_STRONG       = [e.g. 3]
SCHEDULE         = [e.g. Tue and Thu, 9am, with timezone]
DATA_SOURCE      = [how you read trends, see below]
```

**Pick a data source before first run.** TikTok and Instagram don't expose trending feeds freely. Options, easiest first:
1. A paid trend-tracking service with an API or export
2. TikTok Research API (free, restricted, requires an application)
3. A scraping service (usage-based, check the platform's terms)
4. Browser automation (fragile, not recommended)

Web search alone surfaces trends late. Expect "rising" to be less reliable without a real feed.

## Inputs

- Trend candidates from DATA_SOURCE over LOOKBACK
- `posted-trends.json`
- Optional: a few reference links a human flagged as "this is the kind of thing we want," to calibrate taste

## Workflow

1. **Pull** trending TikTok and Instagram content from LOOKBACK.
2. **Filter** for NICHES and BRAND_FIT.
3. **Dedupe before drafting.** Read the state file. Drop any candidate whose `id` already appears. An ID match is a skip, no judgment call. Do not write angles for trends you're about to drop.
   - `id` = the most stable identifier available: the platform's audio or video ID from the URL, else a lowercase hyphenated slug of the trend name.
4. **Assess each survivor:**
   - Rising or peaked? Prefer rising. Flag anything 2+ weeks old.
   - On-brand? Skip anything in OFF_LIMITS.
   - Audio? If yes, the clearance line is mandatory.
5. **Write one creative angle** per trend: one sentence on how your brand could adapt it.
6. **Fill the frozen template** and post to POST_DESTINATION. Show the digest first unless the channel owner has waived review.
7. **Update state** after a successful post: append `{ "id", "name", "date_posted" }` per trend.
8. If fewer than MIN_STRONG strong matches, say so in the post: "Slim week, only [N] strong matches found."

## Rules

- **Audio clearance is not optional.** Every audio trend gets this exact line, verbatim, never paraphrased:
  `⚠️ Sound must be cleared for commercial use via TikTok Commercial Music Library before posting.`
  Brand accounts can't use most trending sounds that personal accounts can. Posting an uncleared sound risks takedowns and legal exposure.
- **Humor has to be funny.** Popular is not enough. When in doubt, skip.
- **Dedupe is mechanical.** Never re-post an ID in the state file, even if it's still rising. A human can ask for a repeat.
- **Post failed means state untouched.**
- **Scheduled runs never wait for a human reply.**

## Output format

Frozen template. Fill bracketed slots only; no new sections, no reworded labels.

```
📱 Northwind Apparel Trend Scout, March 3, 2026

1. [Trend name]
Platform: TikTok | Category: Trending Audio
Link: [url]
Creative angle: [one sentence]
⚠️ Sound must be cleared for commercial use via TikTok Commercial Music Library before posting.

2. [Trend name]
Platform: Instagram | Category: Trending Copy Format
Link: [url]
Creative angle: [one sentence]
```

Example angle: "Use the 'things I'd never wear... until now' format to show three pieces from the new drop styled three ways."
