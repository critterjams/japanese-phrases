# Japanese phrases

A phone-friendly phrase sheet for travel in Japan, hosted at https://critterjams.github.io/japanese-phrases/. It works offline once opened.

Everything is plain HTML, CSS and JS. There is no build step and no dependencies. Open `index.html` in a browser to run it locally.

## Files

- `index.html`: the page, its styles, and all phrase data
- `sw.js`: service worker that caches the page for offline use
- `manifest.webmanifest`, `icon.svg`: let people add it to their home screen

## Publishing

GitHub Pages serves the `main` branch from the repo root. Push to `main` and the site updates in about a minute. There is nothing else to deploy.

Before each push:

- Update the date in `<p class="updated">` in `index.html`. It is typed by hand.
- `CACHE` in `sw.js` does not need a bump for content edits, because the worker fetches from the network first and only falls back to the cache offline.

## Editing phrases

Phrases live in the `sections` array at the top of the main script. Each section has an `id`, a `title`, a Japanese subtitle `jp`, an optional `note`, and `groups`. Sections appear in the dropdown in array order.

A phrase is an array:

```js
[japanese, phonetic, english, flag, spoken, color]
```

- `flag`: `"hear"` tags a phrase staff will say to you ("You'll hear this"). Use `null` otherwise.
- `spoken`: what the voice reads aloud when it should differ from `japanese`, for example an address or text containing "ANA". Defaults to `japanese`.
- `color`: chips only. A CSS color for the swatch next to the English.

Groups render as full-width cards by default. Set `chips: true` on a group to render small tap tiles instead (numbers, signs, colors). A section can also have `counts` for a labeled row of chips.

Cards show English, then Japanese, then the phonetic line. The phonetic line is read aloud by the person traveling, so write it as English syllables.

## Phonetic spelling

Follow the Sounds guide panel in the page. Vowels are `ah`, `eh`, `ee`, `oh`, `oo`. The "eye" sound is spelled `sigh`, `guy`, `zye`, `rye`, `tie` or `kigh`. A final unstressed "u" is `ss` or `dess` style (`mahss`, `dess`). Join syllables with hyphens and separate words with spaces.

## Voice

Speech uses the browser's built-in text-to-speech at 0.8 speed. Voices come from the device, so what plays offline depends on which Japanese voices are installed. If a device has two or more, a mic icon in the top bar lets the user choose, and the choice is saved in `localStorage` under `jpVoice`.
