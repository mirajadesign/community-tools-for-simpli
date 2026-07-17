# Cost Tracker for Simpli

A free, plug-and-play cost calculator for **Simpli Studio**. It tells you the
all-in monthly cost of running each **Page**, not just your Simpli bill, across
every content type, and when it's time to buy top-up minutes or move up a plan.

Made for the Simpli community. No account, no sign-up, nothing leaves your browser.

> **Unofficial and community-made.** This is not affiliated with, endorsed by, or
> released by Simpli Studio or its creator. It's a helper built by a fellow user.

First-time here? The dashboard opens with a short **setup walkthrough** that asks
a few plain questions and builds it for you, including how you'd like your real
spend filled in (let Claude read your Simpli billing, or type it yourself). You
can skip it and edit everything directly, or reopen it anytime with "Setup
walkthrough" at the top right.

## What it does

- Shows a **grand total** up top with everything included (Simpli plan, top-ups,
  fal, voice, Community, scheduler, LLM, anything else) and a line-by-line
  breakdown grouped into Simpli / your keys / other tools.
- **Estimates** each Page's monthly cost from its **content lines**. A line is one
  kind of thing the Page makes: a **reel** built from images, an **image post** or
  banner, an **animation**, a **lip-sync video**, or a **prompt-to-video**. Each
  line has its own count per day, length, images, and quality tier (**Good /
  Better / Best**), so one Page can make a 60s reel, two 30s reels, and a
  Best-quality lip-sync special side by side.
- Separates the two things that drive cost:
  - the **Simpli subscription**, a flat fee that meters a monthly **video-minute
    cap**. Reels, lip-sync, and prompt-to-video use it; image posts and
    animations don't, and
  - your **generation keys** (fal for images, animation, and video generation,
    ElevenLabs or Fish.audio for voice), billed on your own accounts. Voice
    scales with length at a per-minute rate.
- Adds a slot for **other monthly costs**: the optional Simpli Community
  membership (~$27), a publishing scheduler (Buffer, Postly), an LLM/AI
  subscription, or anything else flat, so the total is real.
- Splits the subscription across your Pages and shows a true **total per Page per
  month**.
- Compares every plan and tells you the **cheapest fit**, warns if a Page uses
  animation on a plan that doesn't include it, and prices top-ups vs an upgrade.
- Optionally **tracks your real spend**: paste the numbers from Simpli's *Plan &
  billing* page and it projects your month-end.

## Two ways to use it

**A. Just open the dashboard.** `assets/cost-dashboard.html` runs standalone.
Open it in any browser, edit the Page cards and plan settings, and read your
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

1. In **Your Pages**, one card per Simpli Page: set its platform, then list what
   it makes as content lines. Each line has a type (reel, image post, animation,
   lip-sync, prompt-to-video), a count per day, a length in seconds, images, and
   a quality tier. Use **+ Add content type** for another line and the × to
   remove one. Add or remove Pages freely.
2. In **Other monthly costs** and **Advanced settings**, pick your current Simpli
   plan and fill in any recurring costs: Simpli Community, your scheduler, an LLM
   subscription, whatever applies.
3. (Optional) In **Track actual spend**, copy from Simpli's *Plan & billing* page:
   video-minutes used, spend by provider (fal / ElevenLabs / Fish.audio), and
   spend by Page.

## The most important tip

The estimate turns reels (plus lip-sync and prompt-to-video) × **length** into
minutes, but Simpli's meter can count re-renders and longer videos, so your real
minutes-per-video may be higher. Work it out from your own billing:

```
real minutes per video = video-minutes used ÷ videos you actually produced
```

Set each reel line's **length (s)** to that number × 60. It changes which plan is
cheapest, so it's worth getting right.

## Advanced: let Claude fill it for you (Claude for Chrome)

If you use the **official Claude for Chrome** extension and you're logged into
Simpli, you don't have to type the actuals by hand. Open your Simpli **Plan & billing** page
in one tab and this dashboard in another, and ask Claude to *"read my Simpli
billing and fill in the cost tracker."* It's a **one-time assisted fill** you
re-run whenever you want fresh numbers, not a live feed. Simpli has no billing
API, so the page has to be screen-read each time, and everything stays in your
browser.

## Notes

- Rates (plans, top-ups, per-image by quality, voice per minute, animation and
  lip-sync and prompt-to-video per second) are editable in Advanced settings.
  Update them if your vendors change pricing. The lip-sync and prompt-to-video
  defaults are rough placeholders; set them from your own provider's pricing.
- Generation keys are billed on your own fal / ElevenLabs / Fish.audio accounts,
  separate from Simpli. Set a spending cap on fal before running automation.
- Upgrading from an older version? Your saved setup migrates automatically: each
  Page's videos, image posts, and animations become content lines the first time
  you open the new dashboard, and a customized voice or animation rate carries
  over. Nothing is lost.
- This tool is not affiliated with Simpli Studio; it's a community helper.
