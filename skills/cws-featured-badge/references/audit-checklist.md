# Audit checklist

Work through every item. Status values: ✅ pass · ⚠️ partial · ❌ fail ·
❓ needs manual check (dashboard/account facts you can't verify from code).
Every status needs evidence: a file:line, an asset path, fetched listing
content, or the user's explicit answer. The "How to verify" column tells you
where to look; adapt to the project's layout.

## A. Eligibility gates (any ❌ blocks nomination outright)

| Item | How to verify |
|---|---|
| A1. Is an extension, not a theme | `manifest.json` has no `theme` key |
| A2. Publisher owns the item | Ask user / dashboard |
| A3. Supports English | Listing language + UI strings |
| A4. Published & public on CWS | Fetch the listing URL; "item not found" = fail |
| A5. No active policy violations | Dashboard → item status; ask user |
| A6. Core features free of login/payment walls | Read the code paths for the headline features; if the popup's primary actions work without auth, pass. Paid *extras* (Pro tiers) are fine — paid *core* is not |

## B. Policy & security compliance

| Item | How to verify |
|---|---|
| B1. All network calls over HTTPS | grep for `http://` in fetch/XHR/WebSocket URLs (localhost in test code is fine) |
| B2. No remote code execution | No `eval` of fetched strings, no remotely-loaded scripts (MV3 also enforces this) |
| B3. No deceptive install/UX tactics | Onboarding & marketing surfaces don't mislead about identity or function |
| B4. Secrets hygiene | No service-role keys, API secrets, or tokens in shipped code; only publishable/anon keys |

## C. Technical best practices

| Item | How to verify |
|---|---|
| C1. Manifest V3 | `"manifest_version": 3` |
| C2. Minimal permissions | Each entry in `permissions`/`host_permissions` maps to a shipped feature. `<all_urls>` needs strong justification (and expect the reviewer to probe it); flag any permission with no code path |
| C3. Modern platform APIs | Service worker (not background page), `chrome.action`, `chrome.scripting`, declarativeNetRequest over webRequest-blocking where applicable |
| C4. bfcache safe | No `unload` listeners anywhere in content scripts; no WebSocket/WebRTC opened from content scripts (background SW is fine) |
| C5. E2E tests exist and run | Test directory + CI or documented test command; run them if cheap |
| C6. Performance hygiene | Content scripts sized sensibly, `run_at` chosen deliberately, no polling loops with sub-second intervals, no main-thread-blocking work on page load |

## D. Privacy

| Item | How to verify |
|---|---|
| D1. Privacy policy exists & is reachable | File in repo and/or URL on listing |
| D2. Policy matches actual collection | Diff the policy's claims against what the code sends off-device (analytics, sync payloads, auth). Undisclosed collection is a blocker |
| D3. Dashboard Privacy tab disclosures | ❓ unless user confirms; list exactly what should be declared based on D2 findings |
| D4. Data minimization | Off-device data limited to what features need; prefer local storage where possible |

## E. User experience

The Featured review judges this qualitatively. Anchor every judgment to the
published values: clear purpose, intuitive setup, easy to use, pleasant design.

| Item | How to verify |
|---|---|
| E1. First-run onboarding | Something intentional happens on install (welcome page, guided popup) that shows the user what they got and how to try it *now* |
| E2. Clear purpose in-product | A first-time user of the popup/UI can tell what the extension does without reading the listing |
| E3. Easy to use | Primary actions ≤2 clicks from the popup; keyboard accessible; states (loading/empty/error) handled |
| E4. Pleasant design | Consistent spacing/type/color system; no default-browser-styled buttons; dark/light handled deliberately. Subjective — justify whatever you assert |
| E5. Permission warnings make sense | Install-time warning list (derivable from manifest) won't scare users relative to the value proposition |
| E6. Sign in with Google (if there's auth) | Only applies if users authenticate; anonymous/local auth is fine |

## F. Store listing quality

| Item | How to verify |
|---|---|
| F1. Description is explicit & value-led | First sentence states the outcome; full description covers what/why/how, not just a feature dump |
| F2. Screenshots: present, 1280×800, real | ≥3 recommended; must show actual functionality, uncluttered; check pixel dimensions |
| F3. Promo tile 440×280 present | Asset exists (repo or dashboard ❓) |
| F4. Marquee 1400×560 present | Optional but expected for featuring candidates |
| F5. Icon: 128/48/16 present, recognizable at 16px | `manifest.json` icons + look at the files |
| F6. Category appropriate | One of the 21; matches what the extension actually does |
| F7. Name follows branding rules | No "Chrome"/"Google", no keyword stuffing, ≤45 chars |
| F8. Repo listing copy ≡ live listing | If both exist, diff them; live wins, flag drift |

## G. Established Publisher prerequisites

| Item | How to verify |
|---|---|
| G1. Publisher identity verified | ❓ Dashboard → Account; give the user the exact steps if unverified |
| G2. Account age & clean history | ❓ Ask; "a few months" minimum of policy-clean publishing |

## Severity guide

- **Blocker**: any A-item ❌; MV2; undisclosed data collection; remote code;
  secrets in the bundle; missing screenshots or description.
- **High-impact**: weak listing copy, missing promo tile/marquee, permission
  over-breadth with a plausible-but-unstated justification, no onboarding,
  bfcache violations (Google actively scans for these), no E2E tests.
- **Polish**: design-consistency nits, optional assets, copy tightening.
