# Our Thing

A private couple's app (Aidan & Bridget) — a single-file PWA (`index.html`) hosted on
GitHub Pages at https://tripod110.github.io/Our-thing/, backed by Firebase Firestore
(shared state in `ourthing/shared`, memory photos as separate docs in `ourthing_photos`).

## Design rules

**Effortless and passive.** The app is a companion, not a destination. Opening it should
take zero decisions: each phone remembers its person, cached state renders instantly,
Firebase syncs quietly in the background. Never block on the network when a saved copy
exists.

**Glanceable.** Home answers "what should we do tonight and how are we doing" in one
look — compiled picks, meters, and progress bars, not raw lists. If the user has to
interpret, compile it for them.

**Warm, not corporate.** This is a gift. Playful copy ("way too long. fix this
immediately ⏰"), themes as personality, hearts and confetti where they earn their
place. Personality is a feature here, not noise.

**Never make them refresh.** Firestore `onSnapshot` pushes every change; no manual
refresh paths. Failure states are quiet — a "showing saved copy" pill, never a blocking
error dialog when the app can still function.

**Remember everything.** Person, theme, quiz completion, saying rotation — all persist
(localStorage per device, Firestore for shared state). Configure once, ever.

**Do less, better.** Every feature request gets asked: does this earn its pixels on a
phone screen? Restraint is the differentiator.

## Conventions

- One file: all HTML/CSS/JS lives in `index.html` (ES module script). No build step.
- iPhone-first: safe-area insets everywhere, bottom tab bar, 16px+ font in inputs
  (prevents iOS zoom), `maximum-scale=1`.
- User text is always `escapeHtml`/`escapeAttr`-ed into templates.
- Date-only strings parse via `parseLocalDate` (never `new Date("yyyy-mm-dd")` — UTC shift bug).
- Event delegation on `#main` uses `main.onclick =` assignment, never `addEventListener`
  (renders would stack duplicate handlers).
- Verify with a local server + browser before every push; syntax-check the module with
  `node --check` after edits.
