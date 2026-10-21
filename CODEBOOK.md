# Codebook: operation classes

Status: DRAFT v0.1. Frozen as v1.0 before October 24, 2026.

This codebook maps a flagged record (a post, video, livestream reference, or
ad) to exactly one operation class. Coding decisions follow the inclusion and
exclusion rules below. When a record fits more than one class, code the
class that matches the primary intent of the content, and note the secondary
class in the notes field.

## Fields kept per coded record

- `operation_class` - one of the four classes below
- `confidence` - high / medium / low, based on evidence completeness
- `actor_type` - candidate-aligned page, official-body impersonator,
  scam monetizer, coordinated cluster member, unaffiliated
- `behavior_tags` - comma-separated tags from the detection screens that
  fired (near_duplicate, synchronized_timing, impersonation,
  audience_anomaly, scam_monetization)
- `surface` - facebook_page, facebook_group, instagram, ad_library,
  external_livestream
- `first_seen` - ISO timestamp of the first observed copy
- `notes` - anything needed to reproduce the decision

## Class 1: counterfeit_official_broadcast

Content that presents itself as an official source of election results or
electoral authority communication without being one.

Include: fake "resultado oficial" livestreams, pages or videos mimicking TSE
branding or broadcaster branding, streams that display fabricated vote
counts.
Exclude: genuine TSE or broadcaster content; commentary content that is
clearly satirical or labeled as opinion; election-night coverage that cites
official results with attribution.

Required evidence: screenshot or archive link, account handle, timestamp.

## Class 2: coordinated_rumor_cascade

Substantively identical or near-duplicate claims appearing across multiple
accounts within a short window, where timing or text similarity indicates
coordination rather than independent reporting.

Include: near-duplicate text clusters with synchronized posting; recycled
2022 vintage fraud claims recirculated as current; copy-paste narratives
appearing across pages and groups in the same hour.
Exclude: independent reposting of genuinely newsworthy wire content;
organic viral spread with substantive variation between copies.

Required evidence: cluster membership list, pairwise text-similarity score,
timing spread.

## Class 3: synthetic_candidate_impersonation

AI-generated or manipulated audio/video/images depicting a candidate or
public official saying or doing something they did not say or do, or a
fabricated persona presented as a real person in a political context.

Include: cloned candidate videos, synthetic personas commenting on the
election, voice-cloned statements.
Exclude: clearly labeled parody; editorial illustration marked as such;
low-quality edits that no reasonable viewer would take as real, unless the
content is being distributed with a claim of authenticity.

Required evidence: media file hash, original source if identified, verdict
from a deepfake detection tool where available, human adjudication note.

## Class 4: paid_content_during_blackout

Political advertising delivered through paid surfaces during the legally
mandated blackout window (October 24, 2026 onward), where such delivery is
itself a TSE violation.

Include: ads from Ad Library with delivery dates inside the blackout;
promoted posts from candidate-aligned or issue-advocacy advertisers during
the window.
Exclude: non-political commercial ads; ads with delivery dates before the
blackout that remain viewable but inactive.

Required evidence: ad archive ID, advertiser name, delivery date range,
impression range.

## Adjudication rule

Every automated label requires a human to read the content before the label
is accepted into the coded set. The system proposes; the researcher
disposes. Disagreements and their resolutions are logged in the notes field
so the evaluation in Phase 3 can measure both detector error and coder
drift.
