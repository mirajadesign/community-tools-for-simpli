# Cost Tracker for Simpli

A free, plug-and-play cost calculator for **Simpli Studio**. It tells you what
each **Page** actually costs to run per month — all in — across every content
type, and when it's time to buy top-up minutes or move up a plan.

Made for the Simpli community. No account, no sign-up, nothing leaves your browser.

> **Unofficial and community-made.** This is not affiliated with, endorsed by, or
> released by Simpli Studio or its creator — it's a helper built by a fellow user.

First-time here? The dashboard opens with a short **setup walkthrough** that asks
a few plain questions and builds it for you — including how you'd like your real
spend filled in (let Claude read your Simpli billing, or type it yourself). You
can skip it and edit everything directly, or reopen it anytime with "Setup
walkthrough" at the top right.

## What it does

- Shows a **grand total** up top — everything included (Simpli plan, top-ups,
  fal, voice, Community, scheduler, LLM, anything else) with a line-by-line
  breakdown grouped into Simpli / your keys / other tools.
- **Estimates** each Page's monthly cost from what it makes: narrated **videos**,
  static **images** (posts / banners), and **animations** — for both the
  **Faceless (TikTok)** and **Social (Facebook, etc.)** strategies.
- Separates the two things that drive cost:
  - the **Simpli subscription**, a flat fee that meters a monthly **video-minute
    cap** — videos and animations use it, images don't, and
  - your **generation keys** (fal for images/animation, ElevenLabs or Fish.audio
    for voice), billed on your own accounts. Quality (**Good / Better / Best**)
    sets the per-image cost.
- Adds a slot for **other monthly costs** — the optional Simpli Community
  membership (~$27), a publishing scheduler (Buffer, Postly), an LLM/AI
  subscription, or anything else flat — so the total is real.
- Splits the subscription across your Pages and shows a true **total per Page per
  month**.
- Compares every plan and tells you the **cheapest fit**, warns if a Page uses
  animation on a plan that doesn't include it, and prices top-ups vs an upgrade.
- Optionally **tracks your real spend** — paste the numbers from Simpli's *Plan &
  billing* page and it projects your month-end.

## Two ways to use it

**A. Just open the dashboard.** `assets/cost-dashboard.html` runs standalone.
Open it in any browser, edit the Page rows and plan settings, and read your
numbers. Everything you type is saved in that browser.

**B. Install it as a skill** so your assistant can set it up and pre-fill it for
you, and so it triggers when you ask cost questions.

## Installing the skill

**Claude desktop / Cowork:** open the shared `.skill` file and click **Save
skill**, then enable it under **Settings → Capabilities**. Then you can say
things like *"what would a new Facebook page cost me"* and it builds the dashboard.

**Claude Code:** unzip the package into your skills directory (e.g.
`~/.claude/skills/cost-tracker-for-simpli/`) so `SKILL.md` sits at its root.

**Or from the marketplace:** `/plugin marketplace add mirajadesign/community-tools-for-simpli`
then `/plugin install cost-tracker-for-simpli`.

## Filling it in

1. In **Per-Page estimate**, one row per Simpli Page: set its strategy
   (Faceless / Social), quality tier, and what it makes — videos/day and length,
   images per video, static image posts/day, and animations/day. Add or remove
   Pages freely.
2. In **Plan, top-ups & other monthly costs**, pick your current Simpli plan and
   fill in any recurring costs — Simpli Community, your scheduler, an LLM
   subscription, whatever applies.
3. (Optional) In **Track actual spend**, copy from Simpli's *Plan & billing* page:
   video-minutes used, spend by provider (fal / ElevenLabs / Fish.audio), and
   spend by Page.

## The most important tip

The estimate turns videos (and animations) × **average length** into minutes, but
Simpli's meter can count re-renders and longer videos, so your real
minutes-per-video may be higher. Work it out from your own billing:

```
real minutes per video = video-minutes used ÷ videos you actually produced
```

Set the **Vid sec** field to that number × 60. It changes which plan is cheapest,
so it's worth getting right.

## Advanced: let Claude fill it for you (Claude for Chrome)

If you use the **Claude for Chrome** extension and you're logged into Simpli, you
don't have to type the actuals by hand. Open your Simpli **Plan & billing** page
in one tab and this dashboard in another, and ask Claude to *"read my Simpli
billing and fill in the cost tracker."* It's a **one-time assisted fill** you
re-run whenever you want fresh numbers — not a live feed. Simpli has no billing
API, so the page has to be screen-read each time, and everything stays in your
browser.

## Notes

- Prices (plans, top-ups, per-image by quality, per-video voice, per-animation)
  are editable — update them if your vendors change pricing.
- Generation keys are billed on your own fal / ElevenLabs / Fish.audio accounts,
  separate from Simpli. Set a spending cap on fal before running automation.
- This tool is not affiliated with Simpli Studio; it's a community helper.
