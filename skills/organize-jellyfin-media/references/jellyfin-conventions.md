# Jellyfin Media Conventions

Use this reference after checking the current official Jellyfin docs when internet access is available.

Official docs:

- Movies: https://jellyfin.org/docs/general/server/media/movies/
- Shows: https://jellyfin.org/docs/general/server/media/shows/

## Shared Rules

- Use metadata-provider titles whenever possible.
- Avoid reserved characters in filenames: `<`, `>`, `:`, `"`, `/`, `\`, `|`, `?`, `*`.
- Add metadata provider IDs for reliable matching:
  - Movie: `Movie Name (year) [metadata provider id]`
  - Series: `Series Name (year) [metadata provider id]`
- Prefer IMDb IDs in this skill: `[imdbid-tt1234567]`.
- Keep external subtitles and audio tracks with the media filename stem plus suffixes, for example `.en.srt`, `.en.sdh.srt`, `.commentary.en.aac`.
- Supported extras folders include `behind the scenes`, `deleted scenes`, `interviews`, `scenes`, `samples`, `shorts`, `featurettes`, `clips`, `other`, `extras`, `trailers`, `theme-music`, and `backdrops`.

## Movies

Canonical movie folder:

```text
Movie Name (Year) [imdbid-tt1234567]
```

Canonical single-version movie:

```text
Movie Name (Year) [imdbid-tt1234567]/
  Movie Name (Year) [imdbid-tt1234567].mkv
```

Canonical multi-version movie:

```text
Movie Name (Year) [imdbid-tt1234567]/
  Movie Name (Year) [imdbid-tt1234567] - 2160p.mkv
  Movie Name (Year) [imdbid-tt1234567] - Extended.mkv
```

The version separator must be space, hyphen, space: ` - `. The prefix before it must match the parent folder character-for-character.

## Shows

Canonical series folder:

```text
Series Name (Year) [imdbid-tt1234567]
```

Canonical season structure:

```text
Series Name (Year) [imdbid-tt1234567]/
  Season 00/
  Season 01/
  Season 02/
```

Use padded season numbers for best results. Do not mix episodes directly in the series root with season folders.

Canonical episode examples:

```text
Series Name (Year) [imdbid-tt1234567] S01E01.mkv
Series Name (Year) [imdbid-tt1234567] S01E01-E02.mkv
Series Name (Year) [imdbid-tt1234567] S02E03 Part 1.mkv
```

Specials belong in `Season 00`.
