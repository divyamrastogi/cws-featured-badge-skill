# Source criteria (verbatim where possible)

Captured 2026-06-11 from Google's published documentation. If a criterion seems
outdated, re-fetch these URLs before relying on it:

- Badges overview: https://support.google.com/chrome_webstore/answer/1050673 (see the "Understand Chrome Web Store badges" section)
- Discovery & featuring: https://developer.chrome.com/docs/webstore/discovery
- Best practices: https://developer.chrome.com/docs/webstore/best-practices
- Program policies: https://developer.chrome.com/docs/webstore/program-policies

## Featured badge

> Extensions must "follow our technical best practices and meet a high standard
> of user experience and design."

- The CWS team **manually reviews** every extension before assigning the badge —
  it is never automatic.
- The review checks adherence to CWS best practices, an "enjoyable and intuitive
  experience, using the latest platform APIs and respecting the privacy of
  users", "among other things."
- Listing quality is an explicit review input: a "clear and helpful" listing
  with "quality images and a detailed description."
- "Publishers can't pay to receive Chrome Web Store badges."

### Nomination preconditions (all required)

1. Item is an **extension** (not a theme)
2. Nominating publisher **owns** the extension
3. Extension **supports English**
4. Extension is **published and public**
5. **No active policy violations**
6. **Core features usable without credentials or payments** (a free tier must
   genuinely demonstrate the extension's value; login-walled or pay-walled core
   functionality disqualifies)

Nomination happens via the form linked from the discovery documentation page
(developer.chrome.com/docs/webstore/discovery) — check that page for the
current link, as Google moves it.

## Established Publisher badge

Granted (not applied for) when both hold:

1. "The publisher's identity is verified" — done in the CWS Developer Dashboard
   (Account tab → verified publisher status; requires a verified website or
   email domain).
2. "The publisher has a consistent positive track record with Google services"
   and "compliance with our Developer Programme Policies." New developer
   accounts need **at least a few months** of clean history — there is no way
   to accelerate this.

## Discovery ranking factors (affect featuring & search even without badges)

The store's curation heuristics consider:

- User ratings
- Usage statistics ("downloads vs. uninstalls over time")
- "The design is pleasant to the eye"
- "The item provides a clear purpose and fills a real user need"
- "The setup and onboarding flow are intuitive"
- "The item is easy to use"
- Search ranking depends on "metadata from your item's listing page" — listing
  completeness directly affects discoverability.
- Editors' Picks are curated on "performance, design, usefulness, relevancy and
  breadth of appeal."

## Best practices referenced by the Featured review

### Compliance & security
- Adhere to the developer program policies
- **Manifest V3** (required for new submissions; MV2 is disqualifying)
- HTTPS for all data transmission
- No deceptive installation tactics

### Privacy
- Disclose **all** collected user data in the dashboard's Privacy tab
- Maintain an accurate, current privacy policy
- Disclosures must match what the code actually does

### Performance
- End-to-end testing (e.g., Puppeteer/Playwright) across browser versions, OSes,
  network conditions
- **Do not break the back/forward cache (bfcache)**:
  - replace deprecated `unload` handlers with `pagehide`
  - keep WebSocket/WebRTC connections out of content scripts (use the background
    service worker)

### User experience
- Onboarding: demonstrate functionality with screenshots and videos
- Persistent UI (e.g., side panels) should "enhance browsing without distraction"
- Support "Sign in with Google" where authentication exists
- Follow permission-warning guidelines (request the minimum; avoid scary
  warnings the feature set doesn't justify)

### Store listing
- Compelling, explicit description of what the extension does
- All required images present: icon, promo tile (440×280), marquee (1400×560),
  screenshots (1280×800)
- Images "clear and uncluttered"
- Appropriate category from the 21 defined options (Accessibility, Art & Design,
  Communication, Developer Tools, Education, Entertainment, Functionality & UI,
  Games, Household, Just for Fun, News & Weather, Privacy & Security, Shopping,
  Social Media & Networking, Tools, Travel, Well-being, Workflow & Planning)
- Extension name follows the CWS branding guidelines (no "Chrome"/"Google" in
  the name, no keyword stuffing)
