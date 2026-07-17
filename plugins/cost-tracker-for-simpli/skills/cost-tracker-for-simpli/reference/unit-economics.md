# Unit economics and the cost model

This is the reasoning behind the dashboard. All figures are generic starting
points; every one is editable in the tool. Verify against your own Simpli
billing before you trust a number.

## Simpli's model in one paragraph

In Simpli Studio a **Page** is a brand or account with its own Style Pack and Brand
Kit. Simpli charges a **flat monthly plan fee** and meters a monthly
**video-minute cap**; the actual generation runs on **your own keys** (fal for
images, animation, and video generation, ElevenLabs or Fish.audio for voice) at
cost. The dashboard describes each Page as a list of **content lines**, one per
kind of thing it makes: **reels** (images narrated into video), **image posts**,
**animations** (first/last frame + animate between), **lip-sync videos**, and
**prompt-to-video**. Each line has its own count per day, length, images, and
quality tier.

## The three cost layers

**1. Simpli subscription: meters video-minutes.**
Each plan includes a monthly pool of rendered video-minutes:

| Plan | Price | Included video min | Animation? |
|---|---|---|---|
| Starter | $19.95 | 45 | no |
| Plus (formerly Automation) | $29.95 | 70 | yes |
| Pro | $99.95 | 275 | yes |

**Reels, lip-sync, and prompt-to-video** consume the cap; **animations and image
posts do not**; both run on your fal key only. (Measured Jul 2026: a Good 5s
animation added ~$0.35 of fal spend and **zero** video-minutes to the cap.) Over
the cap you buy top-up minutes, which roll over. Animation requires the Plus or
Pro plan. (Prices/caps as of writing, editable in the tool.)

**2. Your generation keys: billed per generation on your own accounts (BYOK).**
- **Images / animation frames:** fal. Quality tier sets the per-image cost:
  **Good** (fast, cheap, fine for most), **Better** (more detail/consistency),
  **Best** (sharpest, several times the cost). A common Good rate is ~$0.034/image.
- **Voice:** ElevenLabs or Fish.audio, priced per minute of narration in the
  model. ElevenLabs runs roughly 2x Fish.audio for the same length.
- **Animation** carries a per-second fal compute cost on top of its two frame
  images. **Lip-sync** and **prompt-to-video** are priced per second of output;
  their defaults are rough placeholders you should set from your own provider.

**3. Fixed monthly costs.** Simpli Community membership (optional, ~$27), a
publishing/scheduler subscription (Buffer, Postly...), an LLM/AI subscription, or
anything else flat. The dashboard seeds these as editable prompts.

## Default assumptions in the model

| Input | Default | Notes |
|---|---|---|
| Image cost, Good / Better / Best | $0.034 / $0.08 / $0.15 | Simpli published (Jul 2026); set from your fal bill |
| Voice per minute | $0.075 | about $0.05 per 40s reel, ElevenLabs measured (Jul 2026); Fish.audio ~half |
| Animation per second | $0.07 | from a measured $0.35 Good 5s silent clip; sound ~2x, Best (Seedance) more |
| Lip-sync per second | $0.05 | rough placeholder; set from your provider |
| Prompt-to-video per second | $0.15 | rough placeholder; set from your provider |
| Images per reel | ~10 | one image per script line is common |
| Reel length | 30 s | your *target*; most reels run 15, 30, or 60 s (90 at most); see the swing variable |
| Anim counts toward cap | off | measured: animations don't consume the cap |
| Days per month | 30.4 | average |

Per content line, per day (multiply by days/month for the monthly figure):

```
reel:      keys $ = count × (images × image_cost(quality) + voice_per_min × sec/60)
           cap min += count × sec/60
image:     keys $ = count × images × image_cost(quality)
animation: keys $ = count × (anim_per_sec × sec + 2 × image_cost(quality))   (2 = first/last frame)
           cap min += 0   (unless the anim-counts-toward-cap toggle is on)
lip-sync:  keys $ = count × (lipsync_per_sec × sec + voice_per_min × sec/60)
           cap min += count × sec/60
p2v:       keys $ = count × p2v_per_sec × sec
           cap min += count × sec/60
```

A Page's cost is the sum of its lines; the estimate is the sum of its Pages.

## Why minutes are usually the binding constraint

At ~3 reels/day and ~30s each, one Page runs ~45 video-minutes/month, the whole
Starter pool, while its key spend is only a few tens of dollars on
your own accounts. So the plan's included minutes run out before the fal/voice
bill matters, and each new video-heavy Page pushes you toward top-ups or a bigger
plan. **Image-only Pages (e.g. a Facebook/Social page of static posts) are the
exception:** they use no cap minutes, so they only add key cost, cheap to run
alongside video Pages.

## The swing variable: real minutes per video

The estimate uses your *target* length. Simpli's meter can count more: re-renders,
test renders, videos that run long. If the true figure is 1.2-1.5 min/video
instead of 0.65, several Pages can blow past even a large plan and flip which plan
is cheapest. Derive it from your own billing:

```
real_minutes_per_video = video_minutes_used_this_period / videos_actually_produced
```

Then set each reel line's **length (s)** to `real_minutes_per_video × 60`. The
plan recommendation recomputes automatically. This single reconciliation is the
most valuable thing you can do with the tool.

## How the dashboard allocates cost

- **Subscription** (plan price + any top-ups for the recommended plan) is split
  across Pages by their **share of cap video-minutes**; a Page that renders more
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
- **Prices change**: everything is editable; revisit when vendors change pricing.
