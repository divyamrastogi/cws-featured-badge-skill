# cws-featured-badge — a Claude Code skill

A [Claude Code agent skill](https://docs.claude.com/en/docs/claude-code/skills)
that audits any Chrome extension against the Chrome Web Store **Featured
badge** and **Established Publisher badge** criteria, then produces a
prioritized fix plan to qualify.

Built from Google's published criteria:

- [Chrome Web Store badges](https://support.google.com/chrome_webstore/answer/1050673) (support page)
- [Discovery on the Chrome Web Store](https://developer.chrome.com/docs/webstore/discovery)
- [Best practices](https://developer.chrome.com/docs/webstore/best-practices)

## What it does

1. Gathers evidence from your extension's codebase (manifest, permissions,
   privacy behavior, onboarding, tests, store assets) and from your live
   listing.
2. Audits ~35 items across seven areas: eligibility gates, policy/security,
   technical best practices (MV3, bfcache, permissions), privacy, UX, store
   listing quality, and publisher prerequisites.
3. Produces a scorecard report with evidence per item, blockers vs.
   high-impact improvements, dashboard items you must check manually, and a
   nomination-readiness verdict.

Badges can't be bought — the skill never suggests gaming tactics, only
genuinely meeting the published bar.

## Install

```bash
# personal skills (all projects)
git clone https://github.com/divyamrastogi/cws-featured-badge-skill.git
cp -r cws-featured-badge-skill/cws-featured-badge ~/.claude/skills/

# or project-level
cp -r cws-featured-badge-skill/cws-featured-badge .claude/skills/
```

Then ask Claude Code: *"Is my extension ready for the Featured badge?"*

## Layout

```
cws-featured-badge/
├── SKILL.md                      # workflow + report format
└── references/
    ├── badge-criteria.md         # Google's criteria, verbatim, with sources
    └── audit-checklist.md        # the 7-area, evidence-based checklist
```
