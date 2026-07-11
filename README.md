# Wortschatz — Moin, Deutsch!

A German flashcard app: single page, no build step, installable on your phone, works offline.

## Run it

- **Locally**: open `index.html` in any browser, or serve the folder (`python3 -m http.server`).
- **Deployed**: any static host works. Vercel setup below.

## Deploy to Vercel

1. Go to [vercel.com/new](https://vercel.com/new) and import this repository.
2. Framework preset: **Other** — no build command, no output directory. Deploy.
3. *(Optional, enables the AI features)* In the project settings add an environment variable
   `ANTHROPIC_API_KEY` with your [Anthropic API key](https://console.anthropic.com/), then redeploy.
   The bundled serverless function `api/ai.js` proxies the AI requests so the key never reaches the browser.

Without the key everything still works — the AI buttons fall back to built-in article suffix rules.

## Use it everywhere

- **Install as an app**: the site is a PWA — on Android/Chrome use *Add to Home Screen / Install*,
  on iOS Safari use *Share → Add to Home Screen*. It launches standalone with its own icon.
- **Offline**: a service worker caches the app; your words are stored in `localStorage` on the device.
- **Responsive**: layouts for small phones (320 px+), notched screens (safe areas), landscape, tablet and desktop.

> Note: words live in the browser you saved them in — there is no account/sync between devices.

## Features

- **Spaced repetition** — Leitner-style boxes (repeat failed cards immediately; known cards come back after 1 / 3 / 7 / 21 days)
- **Topics** — toggle categories on/off with the chips above the card deck
- **Rounds ("Pro Runde")** — practice in chunks of 5 / 10 / 15 / 25 cards instead of everything at once; the done screen shows how many cards are still due and starts the next chunk
- **Unlimited words** — add your own words in the *+ Neu* tab
- **AI assist** — type just the German word and the AI fills in the article, translation, example sentence (with English translation) and a grammar note
- **Example translations** — cards with an example sentence show its English translation right below it
- **Search & edit** — full word list with search, inline edit and delete

## Built-in categories

| Category | Cards | Source |
|---|---|---|
| Meine Wörter | 9 | starter words |
| Adjektive | 16 | common adjectives |
| Präpositionen | 14 | prepositions with case notes |
| Sätze & Floskeln | 421 | *Moin, Deutsch! Band II — Sätze & Floskeln* (everyday phrases, 23 chapters: greetings, small talk, bakery, checkout, restaurant, trains, doctor, Amt, phone, work, housing, occasions, Norddeutsch) |
| Grundwortschatz | 621 | *Moin, Deutsch!* Band I word list (30 chapters: articles, pronouns, verbs, numbers, family, time, food, home, body, city, work, clothing, colors, weather & nature, particles, useful nouns/verbs, shopping). 54 entries that already exist in the other categories were left out to avoid duplicate cards; the question words and two separable verbs moved to their own categories |
| W-Wörter | 38 | all German question words: wer/wen/wem/wessen, the wie-combinations (wie viel(e), wie lange, wie oft, wie spät …), warum/wieso/weshalb/wozu, and every wo(r)-compound (womit, worauf, woran, worüber …) — each with an example sentence and a grammar note |
| Trennbare Verben | 16 | separable verbs (abfahren, anrufen, aufwachen, einsteigen, umziehen …) — every card's example sentence shows the prefix split, with English translation and a "trennbar: ich rufe … an" note |

### Notes on the *Sätze & Floskeln* cards

Each card's note keeps the extra context from the book:

- **hören** — a phrase the street says *to you* (cashier, conductor, loudspeaker)
- **sagen** — your line
- no tag — flows both ways
- **Norddeutsch** — Bremen/Hamburg specials

## Project structure

```
index.html            the whole app (UI, styles, data packs, logic)
api/ai.js             Vercel serverless proxy for the AI features
manifest.webmanifest  PWA manifest
sw.js                 service worker (offline cache)
icons/                favicon + home-screen icons
```

Study keyboard shortcuts: `Space` flips the card, `←`/`1` = again, `→`/`2` = knew it.
