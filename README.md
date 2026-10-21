# Brazil 2026 Detection Instruments

Query dictionary, codebook, and detection instruments for the research
program "Monitoring Coordinated Information Operations During Democratic
Events: A Defensive Detection Study of the 2026 Brazilian General Election
Runoff."

Program page: https://oam.berkeley.help

## Status

Draft v0.1. The dictionary and codebook will be frozen as v1.0, with a git
tag, before the campaign blackout begins on October 24, 2026. Changes after
the freeze go through the changelog with a stated reason.

## What this repository is

The instruments our detection pipeline uses against public content:
the Portuguese query panels for the Meta Content Library API, the watchlists
of public pages and groups we monitor, and the codebook that maps flagged
content to operation classes. Releasing them openly is part of the program's
commitment: other research groups and civil-society monitors should be able
to reuse and audit the method.

## What this repository is not

It contains no platform data. No posts, no account content, no engagement
records. Dictionary terms and class definitions only.

## Structure

- `dictionary/` - keyword, phrase, and hashtag panels (Portuguese)
- `watchlists/` - public pages and groups sourced from documented reporting
- `CODEBOOK.md` - operation class definitions with inclusion/exclusion rules
- `methods/detection-overview.md` - the screens and how they are evaluated

## License

MIT for the instruments (see LICENSE). Applies to text and code in this
repository, not to any platform data.
