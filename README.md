# Lexicon Terms — how to put it on your phone

A sibling of Lexicon, for written translators. Same folder discipline: this
**is** the website. Nothing needs building or compiling.

```
index.html              the app, the deck and all 50 drawings, in one file
sw.js                   service worker (makes it work offline)
manifest.webmanifest    tells the phone it is an installable app
icon-*.png              home screen icons
```

All of these must sit **together in one folder**, and `index.html` must keep
that name.

---

## 1. Put it online (once, from a computer)

The app needs a web address — `https://`, not a file on disk. Drag this whole
folder onto **app.netlify.com/drop** and you get an address in a few seconds.
Cloudflare Pages and GitHub Pages work equally well.

Keep it separate from Lexicon: a second Netlify site, its own address. The two
apps store their data under different names, so they will not tread on each
other even if you host them together — but separate addresses make the two home
screen icons behave predictably.

## 2. Install it on the phone

**iPhone:** open the address in Safari (only Safari can install on iOS) → Share
→ **Add to Home Screen**. **Android:** Chrome menu → **Install app**.

It then launches full screen with the lightning icon and works in aeroplane
mode.

## 3. Share it

Send the link. Everyone installs their own copy; timings, weak items and
progress stay on their own device and are never sent anywhere. No server, no
account, no analytics.

---

## What is in it

**113 terms from IEC 62305-3**, in ten cards of ten to twelve. Unlike Lexicon,
each card is one coherent slice of the standard — air-termination, earthing,
bonding, explosive zones — because that is how a document hands terminology to
you.

**Three ways to work a card:**

- **Learn** — a read-through. Every term with both languages, the standard's own
  definition where it gives one, and a drawing. Nothing is timed. Swipe or use
  the arrows.
- **Drill** — the familiar two passes. Pass 1 Russian → English, pass 2 English →
  Russian, prompt → answer aloud → reveal → *Got it* or *Missed*. Anything you
  miss comes round again at the end of the pass. The clock runs across both
  passes and the total is stored, so you can watch yourself get faster.
- **Recall** — the definition appears and you name the term. Offered on cards 1,
  5, 7 and 9, which carry enough definitions to be worth it, and deck-wide from
  **Definitions** on the home screen.

**Typing mode** is chosen on the card screen itself — under the Learn and Drill
buttons there is a line reading *Answer by* **buttons / typing**. (The same
switch is in Settings, called *Answering*.) With typing chosen, the drill gives
you an input box and grades the term for you. An exact answer counts as *got it*; anything else
counts as *missed*, on the view that a written translator has to spell it right.
Case, punctuation and ё/е are still forgiven, and short forms are accepted —
typing `LPS` for *Lightning protection system (LPS)* counts as exact. The two
grade buttons are then replaced by a single **Next**, and the verdict line above
it is tappable: one tap flips the grade if you meant a variant the app does not
know. **Reveal** stays available, so you can skip the typing on any term and
grade yourself as usual. With typing mode off, nothing changes at all.

**Weak items** collect every term you miss, across all cards. They clear
themselves after two clean answers, or you can drill them as a set.

**Glossary** searches all 113 terms in either language, including inside the
definitions.

---

## Adding a new standard later

Send me the Excel file and I will return a new `index.html`. If you ever want to
do it yourself, the deck lives near the end of `index.html` in a line beginning
`var DECK =`. One card looks like this:

```json
{
 "id": "c11",
 "n": 11,
 "title": "Surge protection",
 "titleRu": "Защита от перенапряжений",
 "items": [
  {
   "id": "s4-001",
   "en": "Lightning protection zone",
   "ru": "Зона защиты от молнии",
   "ed": "Zone where the lightning electromagnetic environment is defined.",
   "rd": "Зона, в которой определена электромагнитная обстановка.",
   "img": "spd"
  }
 ]
}
```

- `id` must be unique and must never change — progress and timings are filed
  against it. `s3-` marks IEC 62305-3; use `s4-` for 62305-4, and so on.
- `ed` and `rd` (the two definitions) and `img` are optional. Leave them out
  entirely if there is nothing to put in them.
- `img` names one of the 50 drawings already in the file. To see the names, look
  for `var DIAGRAMS = {` — each key is a name you can reuse, such as
  `rolling-sphere`, `bonding-bar`, `zones-gas`. A term with no drawing simply
  shows none.

Because cards are matched by `id`, a new version never overwrites anyone's
timings or weak items.

## Updating everyone's copy

Replace the files on the host, then change one line in `sw.js`:

```js
const VERSION = 'lexicon-terms-v1.3';   // was v1.2
```

That single change is what tells installed phones a new version exists. People
get it the next time they open the app, or immediately via **Check for updates**
in Settings.

## Keeping your data

**Export** in Settings writes a JSON file with your timings, weak items and
progress. **Import** merges it back — it takes the better of the two records for
each term rather than replacing, so you can move between phones without losing
history.

Everything lives in the phone's browser storage. iOS can clear that if the
device runs very low on space or the app goes unused for a long stretch. Export
occasionally; the accumulated timings are the only part you cannot recreate.

---

## Offline behaviour, precisely

- The app and its icons are cached on the first visit and work with no signal at
  all. The whole deck, every definition and all fifty drawings are inside
  `index.html` — there is nothing else to download.
- The drawings are **SVG**: pictures written as instructions ("line from here to
  here") rather than as photographs. That is why they weigh almost nothing, stay
  sharp at any zoom, and change colour with the light and dark themes.
- The PT typefaces are fetched from Google Fonts on the first online run and
  cached after that. If they never load, the app falls back to whatever the
  phone has, and nothing breaks. For zero dependence on Google, choose
  **system** under Typeface in Settings.

## If you publish it

**Google Play:** PWABuilder (`pwabuilder.com`) turns this address into an
Android package almost automatically; one-time $25 developer fee. **App Store:**
$99 a year, a Mac to submit, and Apple's guideline 4.2 means a plain web wrapper
can be rejected — offline operation and a real icon, which this has, are the
minimum to argue it is a genuine app. Both stores want a privacy policy; yours
is easy, since the app collects nothing and transmits nothing.

## Attribution

Terminology is from IEC 62305-3 and its Russian equivalent, from your own
glossary. The typefaces are **PT Serif**, **PT Sans** and **PT Mono** by
ParaType, under the SIL Open Font License — chosen because they were designed
for exactly this pair of alphabets. The drawings are original and schematic;
they illustrate the concept, not the geometry of any particular installation,
and are no substitute for the figures in the standard itself.
