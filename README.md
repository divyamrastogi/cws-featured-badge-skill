# Chrome Web Store Featured Badge Audit

A [Claude Code plugin](https://code.claude.com/docs/en/plugins) that audits
your Chrome extension against the Chrome Web Store **Featured badge** and
**Established Publisher badge** criteria, then produces a prioritized fix plan
to qualify.

The Featured badge is a human review by the Chrome Web Store team — there's no
application queue you can pay or fast-track your way through. The only lever
is genuinely meeting Google's published bar. This skill tells you exactly
where you stand and what to fix first.

## Why this matters

Featured extensions get preferential placement in Chrome Web Store search and
collections — for most extensions it's the single biggest discoverability
lever available. But the criteria are scattered across support pages,
developer docs, and best-practice guides, and a listing that *looks* fine can
still be silently disqualified by a stale privacy policy, an over-broad
permission, or a screenshot that doesn't show the extension in use.

## What it does

1. **Gathers evidence** from your extension's codebase (manifest, permissions,
   privacy behavior, onboarding, tests, store assets) and from your live
   listing.
2. **Audits ~35 items across seven areas**: eligibility gates,
   policy/security, technical best practices (MV3, bfcache, permission
   minimization), privacy, UX quality, store listing quality, and publisher
   prerequisites.
3. **Produces a scorecard report** with evidence per item, blockers vs.
   high-impact improvements, dashboard items you must check manually, and a
   nomination-readiness verdict.

Built from Google's published criteria:

- [Chrome Web Store badges](https://support.google.com/chrome_webstore/answer/1050673) (support page)
- [Discovery on the Chrome Web Store](https://developer.chrome.com/docs/webstore/discovery)
- [Best practices](https://developer.chrome.com/docs/webstore/best-practices)

Badges can't be bought — the skill never suggests gaming tactics (incentivized
reviews, keyword stuffing), only genuinely meeting the published bar.

## Install

As a Claude Code plugin (recommended):

```
/plugin marketplace add divyamrastogi/cws-featured-badge-skill
/plugin install cws-featured-badge@divyamrastogi-skills
```

Or copy the skill directly:

```bash
git clone https://github.com/divyamrastogi/cws-featured-badge-skill.git

# personal skills (all projects)
cp -r cws-featured-badge-skill/skills/cws-featured-badge ~/.claude/skills/

# or project-level
cp -r cws-featured-badge-skill/skills/cws-featured-badge .claude/skills/
```

## Use

Open Claude Code in your extension's repo and ask things like:

- *"Is my extension ready for the Featured badge?"*
- *"Audit my extension for the Chrome Web Store Featured badge."*
- *"Review my store listing before I submit this update."*

The skill triggers automatically on Featured-badge, CWS-badge, and
listing-quality questions.

## Layout

```
.claude-plugin/
├── plugin.json                   # plugin metadata
└── marketplace.json              # makes this repo installable as a marketplace
skills/
└── cws-featured-badge/
    ├── SKILL.md                  # workflow + report format
    └── references/
        ├── badge-criteria.md     # Google's criteria, verbatim, with sources
        └── audit-checklist.md    # the 7-area, evidence-based checklist
```

## Privacy

The plugin is pure Markdown instructions — no telemetry, no servers, no data
collection. Full policy: [javascriptbit.com/cws-featured-badge/privacy](https://javascriptbit.com/cws-featured-badge/privacy/)

## License

[MIT](LICENSE)
