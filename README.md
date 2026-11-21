# Bingey — Terms of Service and Privacy Policy

The Terms of Service, Privacy Policy and child safety (CSAE) standards of
[Bingey](https://play.google.com/store/apps/details?id=com.jashvantsewmangal.bingey), a free Android app
for sharing lists of films, series, books and games with friends.

**Live at:** https://jashvant27.github.io/bingey-legal/

| Link | Opens |
|---|---|
| `https://jashvant27.github.io/bingey-legal/#terms` | Terms of Service (linked from the app's sign-in screen) |
| `https://jashvant27.github.io/bingey-legal/#privacy` | Privacy Policy (linked from the app and Play Console) |
| `https://jashvant27.github.io/bingey-legal/#child-safety` | Child safety standards (Play Console, Child Safety Standards) |
| `https://jashvant27.github.io/bingey-legal/#delete-account` | How to delete your account and data (Play Console data deletion, Facebook data deletion instructions URL) |
| `…/?lang=nl#privacy` | Any section in a given language |

This replaces the CSAE page on Firebase Hosting (`bingey-csae-policy.web.app`) and the terms text that
Bingey 2.x read from `commons/termsconditions` in the Realtime Database.

## Structure

Everything is in `index.html`: one self-contained page, no build step, no dependencies, no cookies and no
requests to other sites.

- **English is the source** and lives directly in `<main id="doc">`, so the page works without
  JavaScript and the `#terms` / `#privacy` anchors resolve natively.
- **Each translation** is a `<template id="l-KEY" lang="KEY" data-label="…" data-title="…">` after
  `<main>`, with exactly the same elements and ids as the English. `data-label` is the name in the
  language dropdown, `data-title` the browser tab title.
- The small inline script fills the dropdown from `ORDER`, swaps the content of `<main>` for the chosen
  template and scrolls to the hash again.

Locales, matching the app: en, nl, de, fr, es, it, pt, pl, tr, ru, ja, ko, hi.

The page picks a language in this order:

1. `?lang=KEY` in the URL (the hash is kept for the sections the app links to)
2. the visitor's previous choice, remembered in `localStorage` (`bingey-legal-lang`)
3. the browser's `navigator.languages`
4. English

## Editing

1. Change the English in `<main>` first, and update the **Last updated** date.
2. Make the same change in every `<template>`. Keep tags, ids, `href`s and the e-mail address identical;
   only the visible text differs. The section ids (`terms`, `privacy`, `delete-account`, `child-safety`,
   `contact`) must never change, because the app and Play Console link to them.
3. Write literal UTF-8; never use HTML numeric entities (`&#12354;`) for letters.
4. Open `index.html` in a browser and step through every language in the dropdown, on a phone width too.

To add a locale: copy a template, translate it, give it `id="l-KEY"` and `lang="KEY"`, and add `KEY` to
`ORDER` in the script.

## Keeping it accurate

The policy describes Bingey 3.0: an encrypted on-device database synced to Firebase (Authentication,
Realtime Database, Cloud Firestore, Cloud Storage, Cloud Functions, Cloud Messaging, Crashlytics), the
shared BingeBase catalogue, friends seeing each other's lists, TMDB / Google Books / MangaDex / IGDB
lookups, no ads and no analytics. If a release changes what is collected, who can see it or which
services are used, **update this page before that version ships**, along with the Data safety form in
Play Console.

## Deployment

GitHub Pages serves the `main` branch from the repository root (Settings › Pages, "Deploy from a
branch"). Every push to `main` is live within a minute or two; there is no workflow to maintain.
