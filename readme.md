# Wyvern eggs

Server definitions for the Wyvern panel. 340 eggs across 11 categories, including all
four of the games this project is built around — Minecraft (Paper), FiveM, Garry's Mod
and Hytale.

## Layout

```
eggs/<category>/<game>/egg-<name>.{yaml,json}
index/wyvern.json
```

`index/wyvern.json` is what the panel reads. Point `PANEL_EGG_INDEX_URL` at its raw URL.
Each egg's `meta.update_url` points back into this repository, so `p:egg:check-updates`
compares against this copy rather than anyone else's.

`.yaml` files are the native Pelican v3 format, `.json` the older PTDL v2. The panel
imports both. Where upstream shipped an egg in several formats, only the best one was
kept and the filename normalised.

## Provenance

These eggs come from the [pelican-eggs](https://github.com/pelican-eggs) organisation
and are MIT licensed. See `LICENSE` — the copyright notice is Michael Parker's and the
contributors', and it stays that way.

What was changed: `meta.update_url` now points here, duplicate format variants were
collapsed, filenames were normalised to `egg-<name>.<ext>`, and one upstream typo
(`ghcr.io/pelican-egggs/`) was corrected.

What was deliberately **not** changed:

| Left alone | Why |
|---|---|
| `ghcr.io/pelican-eggs/*` image references | real container images. Rewriting the strings would make every install pull something that does not exist. Mirroring the images to our own registry is a separate job — 850 MB for the Java images alone. |
| `author` fields | attribution on MIT-licensed work. Rewriting someone's e-mail address to hide where an egg came from would be misattribution, not rebranding. |

## Refreshing from upstream

Nothing pulls automatically. To take new eggs from upstream, re-run the assembly
scripts in `~/wyvern/tmp/` against fresh clones, then review the diff before pushing —
upstream occasionally changes a startup command or an image tag in ways worth reading.
