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
| **cost-tracker-for-simpli** | Work out what your Simpli Studio setup really costs each month — videos, images, and animations, plus the plan minute cap, your fal / ElevenLabs / Fish.audio key spend, and fixed tools like a scheduler or community membership. Opens a friendly setup walkthrough and a plug-and-play dashboard. |

## Install (one time)

In Claude (Cowork or Claude Code), add this marketplace, then install the plugin:

```
/plugin marketplace add mirajadesign/community-tools-for-simpli
/plugin install cost-tracker-for-simpli
```

(This assumes the repo lives at `github.com/mirajadesign/community-tools-for-simpli`.)
That's it — no account with us, no fee, nothing leaves your machine.

## Getting updates

You install once; updates come from this repo (the "master"). When a new version
is published here:

- **Automatic:** if plugin auto-update / sync is on, Claude checks shortly after a
  session starts and prompts you to reload — or the new version loads next launch.
- **Manual:** run `/plugin marketplace update community-tools-for-simpli`, then
  `/reload-plugins`. You'll get whatever version is current in this repo.

No re-downloading files or chasing links — just pull the latest.

## Prefer not to install anything?

Every tool here is also a plain, self-contained HTML file you can just open in a
browser. Grab `cost-dashboard.html` from
`plugins/cost-tracker-for-simpli/skills/cost-tracker-for-simpli/assets/` and
double-click it. Nothing to install.

## Support this project (optional)

These tools are free and always will be. If they save you money or time and you'd
like to chip in, a tip is appreciated — never required, and nothing is gated
behind it.

- **Venmo (easiest):** [@miraja](https://venmo.com/u/miraja)
- Or enable **GitHub Sponsors** on this repo, or drop any donation URL into
  `.github/FUNDING.yml`.

## Maintainer notes — how to publish an update

1. Make your changes inside `plugins/cost-tracker-for-simpli/`.
2. Bump the `version` in **both**
   `plugins/cost-tracker-for-simpli/.claude-plugin/plugin.json` **and** the entry
   in `.claude-plugin/marketplace.json` (semver — e.g. 0.1.0 → 0.1.1 for a fix,
   0.2.0 for a feature).
3. Commit and push to GitHub. Installed users pull it with
   `/plugin marketplace update` (or automatically).

## License

MIT — see `LICENSE`. Free to use, share, and adapt.
