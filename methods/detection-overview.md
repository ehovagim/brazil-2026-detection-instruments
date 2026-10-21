# Detection overview

How the screens work and how we evaluate them. The codebook (../CODEBOOK.md)
defines the classes; this document defines the machinery and the scoring.

## Screens

**near_duplicate.** Text similarity across records, using character n-gram
overlap with a Jaccard threshold. Raises `near_duplicate` when a pair of
records from different accounts exceeds the threshold within a 24-hour
window. Thresholds are set in Phase 1 against the 2024 baseline window and
frozen before October 24.

**synchronized_timing.** Posting-time clustering across accounts. Raises
`synchronized_timing` when three or more watchlisted accounts post
substantively similar content within a ten-minute window. Chosen to catch
coordinated release rather than organic coincidence.

**impersonation.** String distance between account names and the
institution panel (../dictionary/institutions.txt), combined with branding
signals in media where the API exposes them. Raises `impersonation` on a
name match above threshold plus at least one authenticity claim in the
content.

**audience_anomaly.** Engagement growth inconsistent with the account's own
baseline: follower or reaction growth z-score above 4 within a day, or view
counts on video far out of line with the account's distribution. Uses only
aggregate, platform-provided metrics.

**scam_monetization.** Co-occurrence of results-narrative keywords with Pix
payment solicitation phrases from ../dictionary/scam-phrases.txt.

**seeding.** Flags from our external livestream monitoring (Vigia, covering
Twitch, Kick, and YouTube chat and transcription) are used as seeds: a flag
triggers a Content Library search for cross-posted copies and related
accounts, which is how cross-surface diffusion is measured.

## Evaluation

Phase 3 scores every screen against the researcher-adjudicated coded set.
We report precision and recall per operation class, with detection latency
for the live window, and we publish the confusion patterns where screens
fail. No screen's label enters the coded set without a human reading the
content.

## What we deliberately do not do

No generative models write or rewrite any analyzed text. No screen attempts
deanonymization of private individuals. No content is generated, posted, or
interacted with, on any platform, at any point in the pipeline.
