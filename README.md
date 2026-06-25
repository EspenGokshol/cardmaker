# Card Maker

A small, self-contained web app for designing and printing your own playing cards. Pick a card style, a colour, some artwork, write the rules text, and either print a single card or build up a queue and print a whole sheet at once.

No build step, no framework, no server — it's a single HTML file you can open locally or host anywhere static.

**Live version:** https://espengokshol.github.io/cardmaker/

---

## How this came to be

It started as a one-off: a custom deck for a friend's bachelor party. The idea was a party game in the spirit of a certain monster-collecting trading card game — cards with types, colours, and little challenges to hand out through the day.

The first version was just a hand-built HTML page that rendered the finished deck so it could be printed. That worked, but printing kept fighting back — a stray bundler overlay, cards sliced in half across page breaks, three cards spilling off the edge of an A4 sheet. Fixing the printing led to wanting to *edit* cards instead of hand-writing markup, which led to a live single-card editor. Then: a print queue so several cards could go on one sheet. Then editing cards already in the queue. Then a "None" type with custom colours, toggles for the bits not every game needs, and finally proper artwork — searchable icons and image uploads.

Somewhere in there it stopped being a party-specific tool and turned into a general card maker. That's what lives here.

---

## Features

- **Three card styles** — Standard, Ultimate (dark/gold frame), and Challenge (difficulty rating + distinct emblem).
- **Type-driven colours** — 14 preset types, each generating a full coherent palette (frame, header, emblem, pills) from a single base colour.
- **Custom colour** — pick the "None" type to set any colour via a swatch *or* a hex field, with an optional badge label.
- **Flexible text** — name, category/subtitle, pack/context, and an effect/rules box. Hide the pack and reshuffle pills for games that don't use them.
- **Artwork**, three sources:
  - *Emblem* — a procedural type-disc generated from the card's colour (the default).
  - *Icon* — search the full [game-icons.net](https://game-icons.net) library and drop one in; it recolours to match the card or any colour you choose.
  - *Image* — upload your own; it's auto-downscaled and can crop-to-fill or fit-to-contain.
  - Optionally keep the emblem's ambient background behind an icon or image.
- **Print queue** — add cards (with copies), reorder your set visually, click a thumbnail to edit it, then print the whole queue three-up on A4.
- **Copy card HTML** — grab a single card's markup to paste elsewhere.
- **Local persistence** — your queue is saved in the browser, so it's still there next visit.

---

## Using it

1. Open the live link (or `index.html` locally).
2. Build a card on the left; the preview updates live on the right.
3. **Print this card** prints just the current one. **Add to print** drops it into the queue at the bottom.
4. Build up the queue, then **Print sheet** to print them all at once.
5. Click any queued thumbnail to load it back and tweak it; **Update** saves changes, **Add as new** keeps the original.

### Printing tips

- Use the browser's print dialog at **100% / Default** scale (not "Fit to page").
- Turn **Background graphics** on, or the coloured frames and emblems won't print.
- The layout targets **A4 portrait**, three cards per row. If a card crowds the edge on your printer, nudge the page margin in the print CSS.

---

## How it works (tech notes)

- Plain HTML, CSS, and vanilla JavaScript in one file. No dependencies to install.
- Cards are rendered as inline-styled HTML by a single render function per style, so a card is fully self-contained and copy-pasteable.
- The icon picker queries the [Iconify](https://iconify.design) API at runtime and **inlines** the chosen icon's SVG into the card, so a finished/printed card no longer depends on the network.
- Image uploads are downscaled and re-encoded in-browser before being stored, to stay within the browser's local-storage limit.

---

## Privacy

Nothing you create is collected, tracked, or sent to a server — there's no account, analytics, or cookies. Your work in progress (the print queue) is saved locally in your own browser and never leaves your device; clearing browser data or switching browser/device starts fresh.

The page does make two kinds of outbound requests: loading the web fonts from Google Fonts, and — only while you're searching for an icon — querying the Iconify icon API.

---

## Credits

- **Icons:** [game-icons.net](https://game-icons.net), by their respective authors, licensed under [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/). Icon search is powered by the [Iconify](https://iconify.design) API.
- **Fonts:** Anton, Outfit, and Space Mono via Google Fonts (SIL Open Font License).
