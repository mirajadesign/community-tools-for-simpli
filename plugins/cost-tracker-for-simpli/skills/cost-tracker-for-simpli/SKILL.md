---
name: cost-tracker-for-simpli
description: >-
  Estimate and track what it costs to run Simpli Studio Pages across every
  content type: narrated reels, static images (posts / banners), animations,
  lip-sync videos, and prompt-to-video, for both the Faceless (TikTok) and
  Social (Facebook, etc.) strategies. Covers the subscription video-minute cap,
  per-Page generation-key spend on your own accounts (fal for images/animation,
  ElevenLabs or Fish.audio for voice), quality tiers (Good / Better / Best), and
  fixed monthly costs like the Simpli Community membership, a publishing
  scheduler, or an LLM subscription. Use whenever someone wants to know what a
  Page costs to run per month, budget a new Page before building it, compare
  Simpli plans, or decide when top-up minutes or a plan upgrade is worth it.
  Triggers on: "what does my page cost", "cost per page", "Simpli cost",
  "Simpli plan", "am I going to go over my minutes", "should I upgrade to Plus
  or Pro", "top up minutes", "cost to run a Simpli page".
---

# Cost Tracker for Simpli

> Unofficial, community-made. Not affiliated with, endorsed by, or released by
> Simpli Studio or its creator.

A plug-and-play cost dashboard for **Simpli Studio**. It answers one question
honestly: **what does each Page cost to run per month, all in?**

It follows Simpli's own model. In Simpli, a **Page** is a brand or account (it has
its own Style Pack and Brand Kit). The dashboard describes what a Page makes as
**content lines**; each line is one kind of output with its own count per day,
length, images, and quality tier:

- **Reel**: images narrated into a faceless video. The bread-and-butter type.
- **Image post**: standalone images, used as static posts or banners.
- **Animation**: animate between a first and last frame (Plus / Pro plans).
- **Lip-sync video**: a talking-head style clip synced to voice.
- **Prompt-to-video**: straight text-to-video generation.

One Page can hold several lines at once, e.g. one 60s reel, two 30s reels, and a
Best-quality 60s lip-sync subscriber special per day.

## The two cost layers (plus fixed tools)

1. **The Simpli subscription**: a flat monthly fee that meters a **video-minute
   cap** (Starter 45 · Plus 70 · Pro 275 as of writing; Plus is the plan Simpli
   renamed from "Automation" in Jul 2026). **Reels, lip-sync, and prompt-to-video**
   consume the cap; **image posts and animations do not**. Animation needs the
   Plus or Pro plan.
2. **Your generation keys**: billed on your own accounts, at cost:
   - **fal** for images, animation, and video generation. Quality tier (**Good /
     Better / Best**) sets the per-image cost; animation, lip-sync, and
     prompt-to-video are priced per second.
   - **ElevenLabs** or **Fish.audio** for voice, priced per minute of narration
     (ElevenLabs roughly 2x Fish.audio).

Plus **other monthly costs**: the optional Simpli Community membership (~$27), a
publishing/scheduler subscription (Buffer, Postly, etc.), an LLM/AI subscription
if you pay for one, or anything else flat. Seeded as editable prompts so nobody
forgets them.

## What it produces

A single self-contained HTML dashboard (`assets/cost-dashboard.html`) that:

- Leads with a **grand total** ("everything included": Simpli plan + top-ups +
  fal + voice + Community + scheduler + LLM + anything else), grouped into
  Simpli / your keys / other tools, with a line-by-line breakdown.
- Opens first-run with a friendly **setup wizard** (welcome → a fill-method
  **gate** → plan → Pages → other costs → total). The gate asks how they want
  their real spend filled: **auto-assist with Claude for Chrome** (Claude reads
  their Simpli billing and types it in; Pages and other tools stay manual since
  they aren't on the billing page) or **fully manual**. Re-openable via "Setup
  walkthrough." The wizard keeps the quick coarse path (videos / images / mix);
  exact content lines are edited on the dashboard.
- **Estimates** per-Page monthly cost from its content lines (type, count/day,
  length, images, quality); works immediately, no data entry.
- Rolls reels, lip-sync, and prompt-to-video into monthly **video-minutes** and
  checks them against the plan cap; image posts and animations are charged as key
  cost only.
- Splits the subscription across Pages by their **video-minute share** and the
  fixed costs evenly, so each Page shows a true "total / month."
- Flags when projected minutes exceed the plan and prices the top-ups; compares
  every plan and recommends the **cheapest fit**, and warns if a Page uses
  animation on a plan that doesn't include it.
- Optionally **tracks actuals** you paste from the Simpli Plan & billing page
  (video-minutes used, spend by provider, spend by Page).

Everything persists in the browser (localStorage, `scct_` namespace). Saved
setups from older versions migrate to content lines automatically on first open;
nothing is lost. No connectors, no accounts, nothing leaves the machine.

## How to set it up (for the assistant)

1. **Deliver the dashboard.** Copy `assets/cost-dashboard.html` to the user's
   working/outputs folder and present it; it runs standalone in any browser and
   saves under the isolated `scct_` key namespace, so it never collides with
   another cost dashboard's data. **Prefer presenting the file over registering a
   Cowork artifact.** If you do register it as a persisted artifact, give it a
   unique id (e.g. `simpli-cost-estimator`) and **never reuse an existing artifact
   id such as `channel-cost-and-plan`**; reusing an id overwrites that artifact.
2. **Offer to pre-fill.** Ask for their Pages, each Page's strategy (Faceless /
   Social), its content lines (what types it makes, how many per day, lengths,
   images per reel, quality), and current plan, then set the defaults in the
   file's `D` object. If they don't know, ship the defaults; every field is
   editable in the UI.
3. **Point them at actuals.** Tell them what to copy from Simpli's **Plan &
   billing** page into "Track actual spend": video-minutes used, spend by provider
   (fal, ElevenLabs, Fish.audio), and spend by Page.
4. **State the headline** (below) so they read it correctly.

## Optional: assistant-assisted fill (Claude for Chrome)

The dashboard is manual by default and needs no connectors. But if the user has
the **Claude for Chrome** extension and is logged into Simpli, offer to populate
the actuals for them: open their Simpli **Plan & billing** page, read the plan,
video-minutes used, and the by-provider / by-Page spend off the page, and type
those into the "Track actual spend" fields. This is a **one-time assisted fill,
re-run on request, not a standing feed** (Simpli has no billing API, so the page
must be screen-read each time). Never invent numbers; if the page can't be read,
fall back to manual entry.

## The one insight to convey

For most creators the **video-minutes are the binding constraint, not the key
spend.** Key spend on your own accounts is typically a few dollars per Page per
month; the subscription's included minutes run out first. Because **image posts
don't touch the cap**, a Social/Facebook Page that posts mostly static images is
cheap on minutes but adds fal cost, while a Faceless/TikTok Page pumping reels
eats the minute pool fast. The dashboard makes that trade-off visible per Page.

## The swing variable (say this out loud)

The estimate turns reels (and other cap-burning lines) × **length** into minutes,
but Simpli's meter may count re-renders and longer videos, so the real
minutes-per-video can be higher than target length implies. Derive it from your
own billing: **(video-minutes used) ÷ (videos actually produced)**, then set each
reel line's **length (s)** to match. The recommendation re-resolves automatically.

## Honest caveats

- Generation keys vary with prompt length and image count; treat per-minute and
  per-image figures as averages. Set them from your own fal / ElevenLabs /
  Fish.audio bills.
- Voice is priced per minute (default about $0.05 per 40s reel, ElevenLabs
  measured Jul 2026; Fish.audio roughly half). Longer reels cost proportionally
  more voice than older versions estimated.
- Animation was measured (Jul 2026): a Good 5s silent clip added ~$0.35 of fal
  spend and **zero** video-minutes, so the default treats animation as fal cost
  only (not counted against the cap). Sound roughly doubles it, 10s roughly
  doubles it, and Best (Seedance) costs more; all editable. Confirm against your
  own billing.
- The lip-sync and prompt-to-video per-second defaults are rough placeholders,
  not measured; tell the user to set them from their own provider's pricing.
- Plan and top-up prices, quality-tier costs, and included minutes are all Simpli
  values as of setup and are editable; update them if Simpli changes pricing.

## Files

- `assets/cost-dashboard.html`: the standalone dashboard. This is the deliverable.
- `reference/unit-economics.md`: generic cost benchmarks, the per-line cost
  shapes, how the minute cap behaves per content type, and the reasoning behind
  the model.
- `README.md`: human-facing install and usage guide to pass along.
