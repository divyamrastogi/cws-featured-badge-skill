---
name: cws-featured-badge
description: Audit any Chrome extension against Chrome Web Store Featured-badge and Established Publisher badge criteria, and produce a prioritized fix plan to qualify. Use this whenever the user mentions the Chrome Web Store Featured badge, getting an extension featured, CWS badges, store listing quality review, badge readiness, extension discoverability, or asks "is my extension ready for the Web Store" — even if they don't say the word "badge". Also use it before any Chrome Web Store submission or major listing update to catch disqualifying issues early.
---

# Chrome Web Store Featured Badge Audit

Audit a Chrome extension codebase + store listing against Google's published
criteria for the **Featured badge** (manually reviewed by the CWS team) and the
**Established Publisher badge** (granted on publisher standing), then produce a
report with a prioritized fix plan.

Two facts shape every audit:
1. **Badges cannot be bought or expedited.** The only lever is genuinely meeting
   the criteria. Never suggest gaming tactics (incentivized reviews, keyword
   stuffing); these violate program policies and disqualify the extension.
2. **Featured is a human review.** The reviewer checks best-practice adherence,
   UX quality, modern platform APIs, privacy respect, and listing quality. The
   audit must therefore judge *quality*, not just tick boxes — "has screenshots"
   passes a checklist; "screenshots are clear, uncluttered, and show real
   functionality" passes a review.

## Workflow

### 1. Gather evidence

Collect before judging. From the codebase (ask the user for the repo path if
not obvious):

- `manifest.json` — manifest version, permissions, host permissions, name,
  description, icons
- Privacy policy file/URL and what data the code actually collects (search for
  network calls, analytics, storage of user data)
- Onboarding surfaces: first-install pages, popup, options page
- Test setup (E2E tests count toward the "tested across environments" practice)
- bfcache hazards: `unload` handlers, WebSocket/WebRTC in content scripts
- Store assets: icon sizes, screenshots, promo tile (440×280), marquee
  (1400×560), listing copy if checked into the repo

From the user (these live in the CWS dashboard and usually aren't in the repo):
publisher verification status, account standing, current listing text/category,
rating and review count, whether core features need login/payment. If the
extension is published, fetch its public listing page to assess copy,
screenshots, rating, and category directly. Don't guess at dashboard-only
facts — mark them "needs manual check" instead.

### 2. Audit against the criteria

Read `references/audit-checklist.md` and work through every item. For each,
record status — ✅ pass / ⚠️ partial / ❌ fail / ❓ needs manual check — with
**evidence** (file:line, asset path, or fetched listing content), never bare
assertions. The checklist covers seven areas:

1. Eligibility gates (the nomination preconditions — any ❌ here blocks everything)
2. Policy & security compliance
3. Technical best practices (MV3, permissions minimization, performance, bfcache)
4. Privacy (disclosures match actual behavior)
5. User experience (onboarding, intuitive use, clear purpose)
6. Store listing quality (copy, images, category, branding)
7. Established Publisher prerequisites

`references/badge-criteria.md` holds the verbatim source criteria with URLs —
cite it when the user questions why an item matters.

### 3. Report

ALWAYS use this structure:

```
# CWS Badge Readiness — <extension name> v<version>

## Verdict
One paragraph: ready to nominate / nearly ready / not ready, and the single
biggest blocker.

## Scorecard
| # | Area | Status | Evidence |
(one row per checklist item, grouped by the seven areas)

## Blockers (must fix before nominating)
Numbered, each with: what fails, why it matters to the reviewer, concrete fix.

## High-impact improvements (won't block, but reviewers look here)
Same format. Quality-of-listing and UX-polish items usually land here.

## Needs manual check
Dashboard-only items the user must verify, each with exact steps (where to
click in the CWS Developer Dashboard).

## Nomination
If ready: link to the nomination steps in references/badge-criteria.md.
If not: the shortest path to ready, as an ordered task list.
```

### 4. Offer to fix

After the report, offer to implement code-side fixes (listing copy drafts,
manifest changes, bfcache fixes, onboarding improvements). Don't start fixing
without a go-ahead — the user may only want the assessment.

## Judgment calls

- **Severity honesty**: an item is ❌ only if it clearly fails the published
  criterion. Style opinions go to "high-impact improvements", not blockers.
- **The criteria say "among other things"** — Google's review isn't exhaustive
  in public docs. When the extension does something the docs don't address,
  judge it by the review's stated values: enjoyable, intuitive, modern APIs,
  privacy-respecting. Say so explicitly when you're extrapolating.
- **Listings rot**: if listing copy in the repo differs from the live listing,
  the live listing is what the reviewer sees — flag the drift.
