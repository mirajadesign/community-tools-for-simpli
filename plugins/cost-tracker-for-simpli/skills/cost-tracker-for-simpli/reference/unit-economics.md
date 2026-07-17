# Unit economics and the cost model

This is the reasoning behind the dashboard. All figures are generic starting
points — every one is editable in the tool. Verify against your own Simpli
billing before you trust a number.

## Simpli's model in one paragraph

In Simpli Studio a **Page** is a brand or account with its own Style Pack and Brand
Kit. A Page produces three content types: **videos** (narrated), **images**
(standalone posts / banners), and **animations** (first/last frame + animate
between). Simpli charges a **flat monthly plan fee** and meters a monthly
**video-minute cap**; the actual generation runs on **your own keys** (fal for
images/animation, ElevenLabs or Fish.audio for voice) at cost.

## The three cost layers

**1. Simpli subscription — meters video-minutes.**
Each plan includes a monthly pool of rendered video-minutes:

| Plan | Price | Included video min | Animation? |
|---|---|---|---|
| Starter | $19.95 | 45 | no |
| Plus (formerly Automation) | $29.95 | 70 | yes |
| Pro | $99.95 | 275 | yes |

**Videos** consume the cap; **animations and images do not** — both run on your
fal key only. (Measured Jul 2026: a Good 5s animation added ~$0.35 of fal spend
and **zero** video-minutes to the cap.) Over the cap you buy top-up minutes,
which roll over. Animation requires the Plus or Pro plan. (Prices/caps as
of writing, editable in the tool.)

**2. Your generation keys — billed per generation on your own accounts (BYOK).**
- **Images / animation frames:** fal. Quality tier sets the per-image cost —
  **Good** (fast, cheap, fine for most), **Better** (more detail/consistency),
  **Best** (sharpest, several times the cost). A common Good rate is ~$0.034/image.
- **Voice:** ElevenLabs or Fish.audio, per narrated video, billed per character.
- **Animation** also carries a per-animation fal compute cost on top of its two
  frame images.

**3. Fixed monthly costs.** Simpli Community membership (optional, ~$27), a
publishing/scheduler subscription (Buffer, Postly...), an LLM/AI subscription, or
anything else flat. The dashboard seeds these as editable prompts.

## Default assumptions in the model

| Input | Default | Notes |
|---|---|---|
| Image cost, Good / Better / Best | $0.034 / $0.08 / $0.15 | Simpli published (Jul 2026); set from your fal bill |
| Voice per video | $0.05 | ElevenLabs, measured ~$0.05/reel (Jul 2026); Fish.audio ~half |
| Animation cost each | $0.35 | Good, 5s, silent — measured; sound ~2×, 10s ~2×, Best (Seedance) more |
| Images per video | ~10 | one image per script line is common |
| Average video length | 40 s | your *target*; see the swing variable |
| Anim counts toward cap | off | measured: animations don't consume the cap |
| Days per month | 30.4 | average |

Per Page, per month:

```
video_min  = videos/day × days × avg_sec/60
anim_min   = anims/day × days × anim_sec/60          (only added to cap if you toggle it on)
cap_min    = video_min                               (+ anim_min only if the toggle is on; default off)
fal_images = videos × images/video + image_posts + anims × 2   (2 = first/last frame)
keys $     = fal_images × image_cost(quality) + anims × anim_cost + videos × voice_per_video
```

## Why minutes are usually the binding constraint

At ~3 videos/day and ~40s each, one Page runs ~55–60 video-minutes/month — most
of a small plan's pool — while its key spend is only a few tens of dollars on
your own accounts. So the plan's included minutes run out before the fal/voice
bill matters, and each new video-heavy Page pushes you toward top-ups or a bigger
plan. **Image-only Pages (e.g. a Facebook/Social page of static posts) are the
exception:** they use no cap minutes, so they only add key cost — cheap to run
alongside video Pages.

## The swing variable: real minutes per video

The estimate uses your *target* length. Simpli's meter can count more — re-renders,
test renders, videos that run long. If the true figure is 1.2–1.5 min/video
instead of 0.65, several Pages can blow past even a large plan and flip which plan
is cheapest. Derive it from your own billing:

```
real_minutes_per_video = video_minutes_used_this_period / videos_actually_produced
```

Then set "Vid sec" to `real_minutes_per_video × 60`. The plan recommendation
recomputes automatically. This single reconciliation is the most valuable thing
you can do with the tool.

## How the dashboard allocates cost

- **Subscription** (plan price + any top-ups for the recommended plan) is split
  across Pages by their **share of cap video-minutes** — a Page that renders more
  minutes carries more of the plan. Image-only Pages carry little or none.
- **Fixed costs** are split **evenly** per Page.
- **Keys** are charged directly to the Page that generated them.

Each Page's "Total / month" = its key spend + its minute-weighted slice of the
subscription + its even slice of fixed costs.

## Plan decision logic

For every plan: `all_in = plan_price + topup(cap_min − included) + total_keys +
total_fixed`. Top-up cost is the cheapest combination of tiers that covers the
overage (minutes roll over). Lowest `all_in` wins, and the tool warns if any Page
uses animation on a plan that doesn't include it. Upgrading only pays once the
top-ups you'd otherwise buy exceed the price gap to the bigger plan.

## General principles

- **Measure all-in per Page**, including the tools around Simpli, not just the
  headline subscription.
- **Reconcile estimate against actuals monthly** and tune the assumptions.
- **Set a spending cap on your fal account** before running automation.
- **Prices change** — everything is editable; revisit when vendors change pricing.
