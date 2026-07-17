# Community Tools for Simpli

A free marketplace of Claude plugins for people who create with **Simpli Studio**.
Add it once and you can install (and keep updated) any tool inside it.

> **Unofficial and community-made.** Community Tools for Simpli is **not affiliated
> with, endorsed by, or released by Simpli Studio or its creator.** It's built by a
> fellow user to help other creators. "Simpli Studio" is used only to describe what
> the tools work with.

## Plugins in this marketplace

| Plugin | What it does |
|---|---|
| **cost-tracker-for-simpli** | Work out what your Simpli Studio setup really costs each month: videos, images, and animations, plus the plan minute cap, your fal / ElevenLabs / Fish.audio key spend, and fixed tools like a scheduler or community membership. Opens a friendly setup walkthrough and a plug-and-play dashboard. |

## Install (one time)

In Claude (Cowork or Claude Code), add this marketplace, then install the plugin:

```
/plugin marketplace add mirajadesign/community-tools-for-simpli
/plugin install cost-tracker-for-simpli
```

(This assumes the repo lives at `github.com/mirajadesign/community-tools-for-simpli`.)
That's it, no account with us, no fee, nothing leaves your machine.

## Getting updates

You install once; updates come from this repo (the "master"). When a new version
is published here:

- **Automatic:** if plugin auto-update / sync is on, Claude checks shortly after a
  session starts and prompts you to reload, or the new version loads next launch.
- **Manual:** run `/plugin marketplace update community-tools-for-simpli`, then
  `/reload-plugins`. You'll get whatever version is current in this repo.

No re-downloading files or chasing links, just pull the latest.

## What's new

**v0.1.3**
- When you fill in your actual spend, the dashboard now shows it against your estimate: an "actual so far" line up top and a minutes-used-vs-cap and key-spend summary in the Track actual spend section.

**v0.1.2**
- Redesigned "Your Pages" into a card per Page, dropping the wide table and horizontal scroll, with plain-language rows and a live reel-to-images estimate.
- The setup walkthrough now forks: pick "Let Claude do it" and it hands off to the Fill-in-with-Claude flow, or set it up yourself in a quick guided pass.
- Prices calibrated to Simpli's published numbers and real usage: images $0.034 / $0.08 / $0.15 and voice $0.05 per reel.
- Renamed the Automation plan to Plus, matching Simpli, with automatic migration of saved data.
- Added a privacy and FAQ panel on the first wizard step, moved Export PDF into the cost card, fixed whole-number stepping, labeled the Platform and Quality pickers, and made copy-the-prompt work everywhere.
- Reframed around your all-in monthly cost of building your faceless empire the Simpli way: it runs inside Claude and everything is saved on your device.

**v0.1.1**
- Added a "Check for updates" button that compares your copy against this repo and shows the update command.

**v0.1.0**
- First public release: per-Page cost estimate, plan recommendation, actual-spend tracking, and PDF export.

## Prefer not to install anything?

Every tool here is also a plain, self-contained HTML file you can just open in a
browser. Grab `cost-dashboard.html` from
`plugins/cost-tracker-for-simpli/skills/cost-tracker-for-simpli/assets/` and
double-click it. Nothing to install.

## Support this project (optional)

These tools are free and always will be. If they save you money or time and you'd
like to chip in, a tip is appreciated, never required, and nothing is gated
behind it.

- **Venmo (easiest):** [@miraja](https://venmo.com/u/miraja)
- Or enable **GitHub Sponsors** on this repo, or drop any donation URL into
  `.github/FUNDING.yml`.

## Maintainer notes: how to publish an update

1. Make your changes inside `plugins/cost-tracker-for-simpli/`.
2. Bump the `version` in **both**
   `plugins/cost-tracker-for-simpli/.claude-plugin/plugin.json` **and** the entry
   in `.claude-plugin/marketplace.json` (semver, e.g. 0.1.0 to 0.1.1 for a fix,
   0.2.0 for a feature). Also bump `LOCAL_VERSION` in the dashboard (`plugins/cost-tracker-for-simpli/skills/cost-tracker-for-simpli/assets/cost-dashboard.html`) and its `v0.1.x` label to match, so the "Check for updates" button compares correctly.
3. Commit and push to GitHub. Installed users pull it with
   `/plugin marketplace update` (or automatically).

## License

MIT, see `LICENSE`. Free to use, share, and adapt.
