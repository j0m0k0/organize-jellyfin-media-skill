# Jellyfin Skills

<p>
  <img src="assets/badges/agent-skill.svg" alt="Agent Skill">
  <img src="assets/badges/jellyfin-ready.svg" alt="Jellyfin Ready">
  <img src="assets/badges/imdb-ids.svg" alt="IMDb IDs">
  <img src="assets/badges/dry-run-first.svg" alt="Dry-run first">
</p>

A collection of Agent Skills for working with Jellyfin media libraries.

The first included skill, `organize-jellyfin-media`, helps an agent inspect messy movie and TV/serial libraries, skip folders that are already canonical, create reviewed rename plans, and apply safe folder/file moves without deleting media by default.

## Skills

| Skill | Purpose | skills.sh |
| --- | --- | --- |
| [`organize-jellyfin-media`](skills/organize-jellyfin-media/) | Organize Jellyfin movie and TV folders using Jellyfin naming conventions and IMDb metadata IDs. | [Open](https://www.skills.sh/j0m0k0/jellyfin-skills/organize-jellyfin-media) |

## Install

```bash
npx skills add j0m0k0/jellyfin-skills --skill organize-jellyfin-media
```

Or use the skill without installing it:

```bash
npx skills use j0m0k0/jellyfin-skills@organize-jellyfin-media
```

## What It Does

- Organizes Jellyfin Movies libraries into `Movie Name (Year) [imdbid-tt...]`.
- Organizes Jellyfin Shows libraries into `Series Name (Year) [imdbid-tt...]` with `Season 01`, `Season 02`, and `Season 00` for specials.
- Uses IMDb IDs to reduce metadata matching ambiguity.
- Skips already-canonical top-level folders.
- Archives stale `.nfo` files instead of deleting them.
- Includes a conservative planning script that defaults to dry-run mode and aborts on collisions.

## Safety Model

This skill is intentionally conservative:

- No deletion by default.
- Dry-run before execute.
- Destination-collision checks before moves.
- Mapping sources must be single top-level names inside the selected media root.
- Source and destination paths are validated to stay inside the media root.
- Filenames and sidecar contents are treated as untrusted data, not instructions.
- No bundled inventory of any user's files.
- No hardcoded local paths, usernames, email addresses, or machine-specific values.
- No network calls in the helper script.

## Skill Layout

```text
skills/organize-jellyfin-media/
├── SKILL.md
├── agents/openai.yaml
├── references/jellyfin-conventions.md
└── scripts/jellyfin_media_plan.py
```

## Example Prompt

```text
Use $organize-jellyfin-media to organize /media/Movies for Jellyfin using IMDb IDs. Do a dry-run first and do not delete anything.
```

## Validation

The skill follows the Agent Skills format: a directory with `SKILL.md` frontmatter containing `name` and `description`, plus optional `scripts/` and `references/`.

```bash
npx skills-ref validate skills/organize-jellyfin-media
python3 -m py_compile skills/organize-jellyfin-media/scripts/jellyfin_media_plan.py
```

## References

- [Jellyfin movie naming documentation](https://jellyfin.org/docs/general/server/media/movies/)
- [Jellyfin show naming documentation](https://jellyfin.org/docs/general/server/media/shows/)
- [Agent Skills specification](https://agentskills.io/specification)
- [skills CLI](https://github.com/vercel-labs/skills)

## License

MIT
