# Presentation Playbook

The design system and authoring rules behind the decks in this project: how they look, how they are written, how they are built and how they are checked. Where the client's brand and this file conflict, **the brand wins**.

> Version 1.0.

---

## 0. The reference decks

| File | What it is | Weight as a reference |
|---|---|---|
| [`examples/china-iran-war-argument-deck.html`](../examples/china-iran-war-argument-deck.html) | 9 slide argument deck for a group presentation (4 speakers). English. | **Gold standard** for story, data, visuals and step by step reveals |
| [`examples/nubank-scroll-article.html`](../examples/nubank-scroll-article.html) | Scroll based, magazine style web article with sticky graphics, sliders and a phone demo. English. | Reference for the scroll article format |

Both are class assignments, so they show the system on public data, not client work. When unsure how to do something, check how the China deck did it first.

---

## 1. The non negotiables

1. **Client brand first.** If the deck is for or about a company, use that company's fonts, colors, logo and tone (see §4). The house style is only for decks with no client.
2. **Few boxes.** Structure comes from type size, whitespace and thin hairline rules, not from rectangles, cards, pills and shaded panels. No rounded corners. No drop shadows on content.
3. **Visual over verbal.** Show the idea as a number, a chart, a map, a diagram or a working demo. Text only supports it. If a slide is understood from its headline plus one visual, it is right.
4. **No word overload.** One idea per slide or per step. Long content is revealed step by step, never dumped at once.
5. **Every number has a source**, written small underneath it, with a date. Illustrative figures are labelled as illustrative.
6. **Headlines are claims, not topics.** "The Hedge Was Already Paid For", not "EV Market Overview".
7. **No hyphens and no dashes** (-, –, —) anywhere in the deck's text. The author adds one by hand when wanted.
8. **Spanish is always Latin American Spanish** (Mexican), even when presenting in Spain. See §3.3.
9. **Outline first.** Never build HTML before the outline is approved (§6).
10. **One self contained HTML file** that works offline when opened by double click.

---

## 2. Design system

### 2.1 House style (no client brand)

**Backgrounds:** pure white `#FFFFFF` or pure black `#000000`. Pick one as the main surface. Alternating white and black slides is fine for rhythm. No gradients, no textures, no photos behind text.

**Color is meaning, not decoration:**

| Role | Color | Use |
|---|---|---|
| Ink | `#111318` on white / `#FFFFFF` on black | Headlines and body text |
| Secondary text | `#6A7078` | Labels, sources, captions |
| Hairline | `#DCDBD4` on white / `rgba(255,255,255,.15)` on black | Dividers, table rules |
| **Red** | `#D62718`, and `#A81C0B` for small text | **What matters most.** The key number, the conclusion, the active item. 1 to 3 red things per slide at most. |
| **Yellow** | `#FFDE00` | **Warnings and spotlights.** Highlighter behind words (`<mark>`), a deadline, a caveat. Only as a fill, never as text color. |
| **Dark blue** | `#1E3A6E` (adjustable) | **Tone.** Calm structural color: the second series in a chart, section accents, the neutral side of a comparison. |

Everything else stays black or grey. If a slide shows more colors than these, something is wrong.

**Font:** Arial. `font-family: Arial, Helvetica, sans-serif`. No web fonts in the house style.

**Type scale** (1440×810 canvas, taken from China):

| Element | Size | Weight / tracking |
|---|---|---|
| Hero number or date | 96 to 200px | 700, tracking −.045em, line height .9 |
| H1 (cover) | ~96px | 700, −.035em |
| H2 (slide headline) | 52 to 62px | 700, −.03em |
| Big statement or quote | 30 to 54px | 600 to 700 |
| Lead paragraph | 19 to 21px | 400, line height 1.45, secondary ink |
| Body and row text | 15 to 17px | 400, line height 1.4 to 1.5 |
| Eyebrow or label | 11 to 12px | 700, UPPERCASE, tracking .19em, red or grey |
| Source line | 10px | 500, grey |

Always `font-variant-numeric: tabular-nums` on numbers.

### 2.2 Client branded decks

Swap the tokens, keep the grammar.

- **Changes:** fonts, colors, logo, tone of voice, and heading weight if the brand calls for it (a brand with a light heading weight keeps it).
- **Stays:** the stage, hairline structure, eyebrow + headline + visual rhythm, sources, step by step reveals, few boxes.
- **Accent:** the client's accent color **replaces** red and yellow. Emphasis and warnings are done with the client accent (plus weight, size and the highlighter treatment in that accent), not with house red and yellow.
- **Logo:** on every slide except the cover, small, top right, with a light and a dark version depending on the slide background. Applying it as a CSS mask makes recoloring easy.
- **Fonts:** embed brand fonts as base64 woff2 so the file works offline. If a brand font can't be obtained, use the closest free equivalent and say so.

### 2.3 Layout without boxes

Use these instead of rectangles:

- **Hairline rows:** `border-top: 1px solid var(--hair)` on each item, with a two column grid inside (number or label on the left, text on the right). This is the workhorse (China `.mstat`, `.logrow`, `.vrow`).
- **Heavy rule over a group:** `border-top: 2px solid ink` over a 3 or 4 column grid, thin vertical hairlines between columns (China `.roadmap`, `.insights`, `.rebs`).
- **Left accent bar:** 4 to 5px bar left of a thesis or quote (yellow = our claim, ink = the other side's claim).
- **Numbered items:** small red `01 02 03`, a short bold title, a short paragraph.
- **Highlighter:** `<mark>` in yellow behind 1 or 2 key words.
- **Solid color block:** only for the single verdict of the whole deck (China "Advantage Beijing").
- **White card with hairline border:** only when text must sit on top of a busy visual such as a map.

Spacing: generous padding (about 74px top and bottom, 92 to 115px on the sides). Content left aligned. Max text width about 1250px; paragraphs narrower (600 to 900px).

### 2.4 Visuals

- **Charts drawn in code** (CSS or inline SVG), in the deck's own type and colors. Same units, labels directly on the bars, no legends, no gridline clutter. The chart's point is written in the headline.
- **One hero number** can own a slide: huge, alone, in the emphasis color (China `-72%`; the carrier counter dropping to `0`).
- **Maps:** Natural Earth outlines as inline SVG, muted land, one highlighted country, animated routes and arcs, camera moves by animating the viewBox.
- **Product and UI mockups:** redraw the tool (a Word document, a Teams channel, a form) in the deck's own typography. Not a pixel copy; the same idea drawn with the deck's rules. **Exception:** when the audience is learning a tool (training and workshops), the mockup should look like the real app, so people recognise it when they open it.
- **A recurring device:** one visual metaphor that builds across the deck and resolves at the end (China's Ledger: a balance that gains a block after each section and finally tips).
- **Photos, GIFs and short videos are welcome when they beat a coded animation:** team headshots, product photos, product demo recordings. Videos autoplay, muted, looped, no controls. Embed small files as base64; for large videos, ship them in a folder next to the HTML and say so.
- Never: stock photos, emojis, clip art icons, decorative images.

### 2.5 Motion

- Slides move horizontally (transform on a track, about .7 to .8s, eased).
- Revealed elements fade up 14 to 18px.
- Motion always means something: a bar grows to its value, a headline gets struck through, a counter drops to zero. No decorative animation.
- **Every step does exactly one visible thing.** A big moment gets the screen to itself: hide the other panels.
- Respect `prefers-reduced-motion`.

---

## 3. Storytelling and writing

### 3.1 Deck types

The decks fall into a few types: **proposals, workshops, ideas and demos**, and class presentations.

**Proposal pattern**
1. Cover: client name, place, date, logo.
2. The opportunity: why this client is in a special position ("a traditional firm" vs. "you").
3. How it works: an interactive walkthrough of a real day, with the client's own names and cases.
4. The components (for example: agents, access by role, confidentiality, continuous improvement), each as a demo or a clean hairline table.
5. Roadmap with phases and **exit gates** ("you don't move to the next phase without meeting these").
6. Team: who builds it, short credentials, headshots allowed.
7. Investment: one big fee number, payment terms, a slider for third party costs.
8. Options, if any, with a live calculator.
9. Next steps: 3 numbered steps plus the exact list of what we need from them in week one.

**Demo:** same bones as a proposal, but section 3 is the deck. The client clicks through a working mockup of their own process, or a recorded product demo plays.

**Idea / argument (China pattern)**
1. **Thesis first:** show the common view, strike it through, state the counter thesis and the verdict. A roadmap row shows the sections (and speakers, if several).
2. **Make the other side's case** better than they would, with real numbers.
3. Evidence sections, each ending on a turn: a zoom, a reveal, a reversal.
4. **The strongest objection**, stated at its strongest, answered point by point, then a one line verdict.
5. **The non obvious insight.**
6. **What changes on Monday:** concrete recommendations, split by audience.
7. **Close:** the recurring device resolves, the verdict in plain words, an open question for debate.

**Scroll article (see `examples/nubank-scroll-article.html`):** a vertical, magazine style web page instead of slides. No slide transitions; things happen as the reader scrolls (sticky graphics with text steps) or plays (sliders, toggles, a phone demo). Lead with the premise in the first paragraph, one interactive moment per section, sources as small lines under each visual plus a source list in the footer. Same brand, writing and density rules; edit mode still applies.

**Workshop pattern (with few boxes):** agenda, ground rules, one method (e.g. CARE), before and after examples, hands on exercises, common mistakes, a closing "start here".

### 3.2 Writing rules

- **Short, declarative sentences.** "Barrels come back. Structure does not."
- **Headline = the takeaway.** Someone who reads only the headlines gets the whole story.
- **An eyebrow above every headline** that frames the section ("The loss column", "09 · La inversión").
- **A punchline line** can close a slide: one bold sentence under a rule in the emphasis color.
- **Honesty lines:** say what you are not claiming. Label illustrative numbers.
- **No hyphens, no dashes.** Rewrite instead: "US backed", "short term", "20 to 30 years", "julio a agosto", "Semanas 1 a 4". For separators use `·`.
- Numbers written the way the audience reads them (`5.4m`, `39,500 €` or `$39,500` per the audience's convention).

### 3.3 Spanish

- Always **Latin American (Mexican) Spanish**, including in Spain.
- Address the audience as **ustedes**, never *vosotros*; in singular, **usted** for clients and formal settings, **tú** only if the setting is clearly informal.
- Mexican vocabulary: *computadora*, *celular*, *costo*, *agendar*, *platicar*.
- Check tildes, ¿ ¡ and « » or “ ” consistently.

### 3.4 Density

China slides hold 115 to 280 words in total but reveal them in 3 to 5 steps, so about 30 to 60 words show at any moment. Static proposal slides hold 20 to 130 words. Rules:

- **About 60 words visible at once at most** (sources excluded).
- 3 to 5 rows per list, 3 to 4 columns per grid at most.
- If a slide needs more, split it into steps or into two slides.

---

## 4. Client brand research

The client's brand guide is usually not available, so pull it from the web.

1. Start with the **company's official website**: inspect the CSS for font families and color values, and download the logo (SVG preferred).
2. If needed, use brand resource sites (brand guides, press kits, brand databases).
3. **Always report the source of each finding** before building, for example:

| Item | Value | Source |
|---|---|---|
| Primary color | `#00529C` | example.com, site CSS (official) |
| Heading font | Montserrat | example.com, site CSS (official) |
| Logo | SVG | brandsite.com (third party, please check) |

Mark clearly what came from the official site and what came from a third party, so the reader can verify the latter.

Also collect: logo light and dark versions, accent color (it replaces red and yellow), tone of voice.

---

## 5. Technical standard

Every deck is one `.html` file built on the same engine as the China deck:

- **Stage:** fixed 1440×810 (16:9) canvas, scaled to fit the window with `transform: scale()`, letterboxed.
- **Track:** slides in a horizontal row; navigation is `translateX(-i*1440px)`.
- **Slides:** `<section class="s">` with modifiers (`s--wide`, `s--dark`, `s--light`) and `data-label` for the counter.
- **Step by step reveals (standard):** `data-beats="N"` on the slide, `data-b="k"` on its elements, plus an optional per slide hook for choreography. Going back a step reverses cleanly.
- **Edit mode (standard):** opening with `?editar` makes every text editable in place; a bar offers "Save and download", which writes a new HTML file with the changes, restored to its clean start state. Keyboard navigation is off while editing. Content that lives in data arrays is written back to the arrays.
- **Editable data at the top of the script:** names, fees, phases, costs, and so on live in plain JS arrays, so content changes don't touch layout code.
- **Chrome:** clickable slide rail on the left, counter bottom left (`01 / 09`, number only: the eyebrow already names the section, so do not repeat it), arrow buttons bottom right, help overlay listing the keys.
- **Keys:** → / Space / Enter next, ← back, PageUp and PageDown whole slide, Home, End completes the slide, 1 to 9 jump, F fullscreen, ? help.
- **Live counters** (days since, days until) **only when they add to the story.**
- **Idle hint** for decks sent to be read alone: "Use the arrows to advance" after about 8 seconds.
- **Self contained:** fonts, logos and images as base64; no CDN dependencies.
- **No presenter window.**
- `<html lang>` set to the deck's language.

Templates: none yet. Once there are 5 or 6 decks, extract templates per use case (proposal/demo, argument, workshop).

---

## 6. Process

1. **Brief.** Get: audience; what they should think, decide or do; how it is shown (live, sent to read alone, or both); length; number of speakers; language; client brand or house style; deadline. Ask only what isn't already clear.
2. **Brand research** (§4) for company decks, with sources.
3. **Research.** Collect facts with source and date. Nothing unsourced goes on a slide.
4. **Outline for approval. Stop here and wait.** One line per slide: eyebrow, headline as a claim, the one visual, and the steps. Keep it short; no HTML yet.
5. **Build** after approval: engine and tokens, then content, then visuals, then choreography, then edit mode.
6. **QA** (§7).
7. **Deliver** the file with a short note: assumptions, anything not sourced, brand sources.

---

## 7. QA checklist

- [ ] Opens offline by double click in Chrome and Safari.
- [ ] Every slide checked at 1440×810: nothing overflows, overlaps or gets clipped.
- [ ] Every step checked forwards **and** backwards.
- [ ] `?editar` works and the downloaded file opens clean.
- [ ] Every number has a source and a date; illustrative numbers are labelled.
- [ ] The headlines alone tell the story.
- [ ] No hyphens or dashes in the text (search for `-`, `–`, `—` in visible text).
- [ ] Density limits respected (§3.4).
- [ ] Box count: could any card become hairline rows?
- [ ] Colors used only with their meaning (house or client accent).
- [ ] Brand: correct fonts actually rendering, logo correct on light and dark.
- [ ] Spanish: Latin American, ustedes, tildes, ¿ ¡.
- [ ] Media (videos, GIFs) autoplay muted and the file size is reasonable.
- [ ] Reduced motion works.
