# The Frameworks — website prototype

A ten-page HTML/CSS/JS prototype: a homepage built around a scroll-driven
icon sequence that hands over to a normal scrolling page, plus five content
pages, two articles on one template, a case study, and the Brand Proximity
service page. No build step, no dependencies, no framework —
every page is one self-contained file.

```
open index.html
```

That's it. The only external request is Google Fonts (Geist / Geist Mono);
everything else is local. Any static server works if you'd rather serve it —
`python3 -m http.server 8777` is enough.

- **Live:** <https://mwalsh-thf.github.io/the-f-prototype/>
- **Repo:** <https://github.com/mwalsh-thf/the-f-prototype> (GitHub Pages, deploys from `main`)
- **Design:** Figma — "The F website 2026"

### Figma frames

| Page | Frame |
|---|---|
| Homepage | [`2446:55689`](https://www.figma.com/design/8Iz2K9VMKdGd09eOTRl3cQ/The-F-website-2026?node-id=2446-55689) |
| Work | [`2896:11570`](https://www.figma.com/design/8Iz2K9VMKdGd09eOTRl3cQ/The-F-website-2026?node-id=2896-11570) |
| Services | [`2895:10584`](https://www.figma.com/design/8Iz2K9VMKdGd09eOTRl3cQ/The-F-website-2026?node-id=2895-10584) |
| About us | [`2896:11715`](https://www.figma.com/design/8Iz2K9VMKdGd09eOTRl3cQ/The-F-website-2026?node-id=2896-11715) |
| Thinking | [`2896:12136`](https://www.figma.com/design/8Iz2K9VMKdGd09eOTRl3cQ/The-F-website-2026?node-id=2896-12136) |
| Contact | [`2896:12444`](https://www.figma.com/design/8Iz2K9VMKdGd09eOTRl3cQ/The-F-website-2026?node-id=2896-12444) |
| Article | [`2789:434`](https://www.figma.com/design/8Iz2K9VMKdGd09eOTRl3cQ/The-F-website-2026?node-id=2789-434) |
| Case study (collapsed) | [`3113:7185`](https://www.figma.com/design/8Iz2K9VMKdGd09eOTRl3cQ/The-F-website-2026?node-id=3113-7185) |
| Case study (expanded) | [`3107:2283`](https://www.figma.com/design/8Iz2K9VMKdGd09eOTRl3cQ/The-F-website-2026?node-id=3107-2283) |
| Brand Proximity | [`3437:2906`](https://www.figma.com/design/8Iz2K9VMKdGd09eOTRl3cQ/The-F-website-2026?node-id=3437-2906) — Myles' refined frame (3 Sep 2026); the other designer's original is `698:2994` in the separate "Brand-Proximity" file |

The full-site page in Figma is `2895:8392`. ⚠️ `get_metadata` on that node
overflows its response limit — drill into individual frames instead.

## Files

| | |
|---|---|
| `index.html` | **The homepage.** Markup, styles, script in one file. |
| `article.html` | **Article 1** — "Your brand has got the answers". Two sticky images that hand over. See below. |
| `article-2.html` | **Article 2** — "I am challenging: Janelle". Same template, one sticky cover. |
| `case-study.html` | **Case study (botim)** — collapsible story, sticky details column. See below. |
| `brand-proximity.html` | **Brand Proximity** — the service page: hero mosaic, then a four-state sticky stage (Context + three cards) on the homepage's scroll model with a morphing mosaic and overlay cards. Reached from Services. See below. |
| `work.html` | Work index — filterable project grid. |
| `services.html` | Services — icon grid, client logo wall, sortable awards table. |
| `about.html` | About us — team grid, employee-owned, draggable B&W strip. Grey ground (`#DFDFDF`). |
| `thinking.html` | Frame of Mind — the blog index. Dark ground (`#1F1F1F`). |
| `contact.html` | Contact — dark, one viewport, working form. |
| `assets/` | Images. All local; nothing depends on a CDN — see the breakdown below. |
| `v1.html`, `v2.html` | Earlier versions, kept for reference only. Superseded — don't start from these. |
| `handoff/` | **The design system, packaged for someone building a new section elsewhere.** `theframeworks.css` + `theframeworks.js` + a working `starter.html` + `BRIEF.md`. See below. |

### What's in `assets/`

| | |
|---|---|
| `article/` | The two article pages' covers and the LEGO image. |
| `icons/` | The ten service marks. |
| `logos/` | All 30 client logo SVGs for the Services wall. |
| `strip/` | The 13 colour-graded About carousel slides. |
| `team/` | The 21 About headshots. |
| `thinking/` | The 16 Frame of Mind cover images. |
| `casestudy/` | The botim case study's nine media items (2.0MB) — two SVGs, six JPEGs, one PNG. |
| `work/` | The 17 Work tile images. |

`v1.html` and `v2.html` share the same `assets/` folder, which is why
`nav-logo.svg` and `v1-clarity-kuruvilla.png` are still there — `index.html`
doesn't use either.

## Handing the system to another builder

`handoff/` is a self-contained kit for a developer or designer building a new
section outside this repo — including one working with their own AI assistant,
which `BRIEF.md` is written to be read by.

| | |
|---|---|
| `theframeworks.css` | Every token, the type scale, nav, footer, reveal, full-bleed helper and the three breakpoints. Values lifted from the live build, not restated from memory. |
| `theframeworks.js` | The `.js` guard, the row-staggered reveal observer, `TF.commit()`, `TF.staggerByRow()`, the semi-sticky nav and the `--sbw` measurement. |
| `starter.html` | A working page — nav, masthead load-in, 4-col grid, footer — to copy and build inside. |
| `BRIEF.md` | The rules, plus the eleven traps from "Things that will bite you" written as instructions rather than history. |

Zip it from the project root:

```bash
cd ~/Desktop/TheF_Homepage_Prototype_V1/files/frameworks-scroll-prototype && zip -r ~/Desktop/TheFrameworks-design-system.zip handoff
```

⚠️ **The kit is a copy, not a live import.** These seven pages still carry
their own duplicated tokens — that was the original no-build decision and it
hasn't changed. So a change to the system means changing it in eleven
places now (ten pages plus the kit). If the two ever drift, the seven pages are the source of
truth and `handoff/` is the thing to re-cut.

⚠️ `starter.html`'s logo is a placeholder black square. The real F mark is
inline SVG in the nav of any built page — send it, or let them lift it.

## How it behaves

1. **Intro** — hero copy with the icon parked off the bottom edge, only its top
   showing. The icon is larger here and shrinks as you scroll in.
2. **The scroll experience** — five states (Clarity / Proximity / Imagination /
   Empathy / Momentum). A ten-triangle icon translates and rotates between
   keyframes taken from the Figma "Icon State" frames. The nav mark is built
   from the same ten triangles and morphs with it (desktop only).
3. **Hand-off** — once Momentum settles, the document unlocks and the page
   scrolls normally. The experience scrolls away with it; the nav stays.
4. **The page** — selected work grid, logo ticker, contact module, footer.

## The site pages (Work / Services / About / Thinking / Contact)

Figma: page "Claude Full-site" — frames `2896:11570` (Work), `2895:10584`
(Services), `2896:11715` (About), `2896:12136` (Thinking), `2896:12444`
(Contact). Every page repeats the same shell as `article.html` — 2200px cap on
`body`, ground on `html`, fixed 100px `--pad-x`, shared footer, 767px nav
collapse — deliberately duplicated per file, no build step. The nav across all
pages is now: Work / Services / About / Thinking / Contact, each link live,
logo → `index.html`. The current page carries `aria-current`.

⚠️ **The fixed nav subtracts `--sbw` from both its width and its centring**,
and the reason is the same one the full-bleed breakouts document: a fixed
element's containing block is the *initial* containing block, which
includes the scrollbar gutter. A plain `width:100%` therefore spans the
viewport **plus** the scrollbar and overhangs the visible page by exactly
that much, raising a horizontal scrollbar of its own; and once the width is
corrected, `left:50%` still centres against the gutter-inclusive box and
pushes the bar right by `--sbw/2`. Both halves are needed —
`width:calc(100% - var(--sbw,0px))` and
`left:calc(50% - var(--sbw,0px)/2)`. This was latent from the day the nav
went fixed: it is invisible on macOS overlay scrollbars (`--sbw` is 0) and
only showed up under a viewport emulating a classic scrollbar. `index.html`'s
`.scene` is fixed too and takes the same correction; `body.released .scene`
is absolutely positioned against the body's padding box, which has no
gutter, so it is deliberately left alone. Verified flush at scrollbar
widths 0 / 15 / 20.

**The nav is fixed and semi-sticky on every page now**, matching
`index.html`: pinned to the top, hides on the way down, returns the instant
you scroll up, always visible on mobile (it's the only way back to the rest of
the site there). This reverses an earlier, explicit decision for the six
content pages — the nav used to be ordinary in-flow content that scrolled away
— made when the brief was to keep those pages simple; the brief this round was
site-wide consistency instead, so the six pages were brought in line with the
homepage rather than the other way around (the homepage's fixed nav is
load-bearing — it has to outlive the scroll-locked scene beneath it — so that
side of the merge was never in question). Capped and centred exactly like
`index.html`'s own nav (see above); each page's first section gets
`calc(var(--nav-h) + Npx)` of top padding to compensate for the nav no longer
contributing its own height to the document flow.

`index.html` is capped at 2200px too now, but it needed a different technique
from the plain `body{max-width}` the other six pages use, because its nav and
hero are `position:fixed` — a fixed element's containing block is the true
viewport regardless of any ancestor's own `max-width`, so simply capping `body`
would leave the hero full-bleed while the nav sat centred above it, two
different widths visibly split on anything over 2200px. Both `.nav` and
`.scene` (the fixed hero stage) instead use `left:50%; width:100%;
max-width:var(--page-max); transform:translateX(-50%)` — only one horizontal
edge pinned, so there's nothing for `max-width` to fight (the earlier `inset:0`
pins both `left` and `right`, leaving no `auto` margin for centring to resolve
against, which is genuinely a different problem from `.strip-wrap`'s breakout
on the About page below — that one's normal-flow and centres by `margin-inline`
math instead). `body.released .scene` (the post-lock, absolutely-positioned
state) takes the same treatment. `.nav.is-hidden`'s show/hide `translateY`
has to live in the *same* transform declaration as the centring `translateX` —
a later rule's `transform` replaces the whole value rather than composing with
it, so writing `is-hidden` as just `translateY(-100%)` would silently re-flush
the bar to the left the moment it hid.

Everything positioned off `--edge-x` (`.submenu`, `.copy`, `.highlight`,
`.hero-stage`) is a descendant of `.scene`, so it's carried along for free —
no changes needed at their own rules. The one place that genuinely needed a
code change is `fit()` in the script: `--s` (the hero's scale) used to solve
against raw `innerWidth`, which knows nothing about the cap. Past 2200px it
would size the hero for space `.scene` doesn't actually have. `fit()` now
solves against `Math.min(innerWidth, PAGE_MAX)` instead — verified at a
2400×2400 window that `--s` resolves to the capped value (1.3889) rather than
what the raw viewport would give (1.6667).

All "Let's talk" CTAs across the site (homepage, About, Thinking) point at
`contact.html`; Services' already did.

### The logo's half-pixel

The F's seam treatment — a 1px `vector-effect:non-scaling-stroke` in the
fill colour — bleeds 0.5px OUTSIDE the fill on every free edge. The logo's
negative margin used to cancel only the mark's left bearing (13.11px at
52.44, 10px at 40), so the visible edge sat half a pixel left of the page
margin — which reads as "1px out" on a 2x display. The margins are now
`-12.61px` / `-9.5px` (bearing less the bleed), and the ink lands on the
margin exactly: measured 25.0 at 375 on every page. `index.html` keeps its
own mobile inset (its tokens are mirrored in `fit()`), so its mark aligns
to its own content margin rather than the 25px system — deliberate.

### The nav has no bar — it blends

The six content pages used to paint a solid `background:var(--bg)` behind the
fixed nav. That's gone; the bar now sits straight on the page, as
`index.html`'s always has. Legibility comes from **`mix-blend-mode:difference`
on `.nav`**: the bar's ink is subtracted from whatever is under it, so it
inverts against the page ground *and* against imagery as the page scrolls
beneath it.

**The ink values are sources for a subtraction, not the colours you see.**
That's the thing to hold in mind when editing them:

| | source | on #F7F7F7 | on #DFDFDF | on #1F1F1F |
|---|---|---|---|---|
| links | `--mid-grey` 143 | 104 | 80 | 112 |
| logo, hover, current | `#fff` 255 | 8 | 32 | 224 |

Links stay `--mid-grey` so they land on a mid tone whichever way they invert;
the logo and the hover/current state go pure white so they invert to maximum
contrast. That preserves the design's grey-to-high-contrast hover relationship
on light and dark pages alike, which a flat white would not — note the old
light-page hover, `--black` (39), would have inverted to a *paler* tone than
the resting state, i.e. backwards.

⚠️ **Difference has a null point, so this is "adapts to almost anything", not
"always".** A source vanishes where the backdrop is half its value: white
disappears on ~`#808080`, mid-grey on ~`#474747`. None of the three page
grounds are anywhere near those, but B&W photography passing under the bar
can be. If it ever bites, the fallback is a scrim behind the bar — which is
what was just removed, so treat it as a last resort.

⚠️ **The nav's own `transform` does not break this**, and it's worth knowing
why, because the instinct is to assume it does. A transform isolates a
stacking context for an element's *children*; the element itself still blends
with its parent's backdrop. So `.nav`'s centring `translateX(-50%)` is fine —
but blending applied to something *inside* `.nav` would be isolated by that
same transform and silently do nothing. Blend the bar, not its contents.

`index.html` is deliberately untouched: its nav already had no bar, and its
mark is the morphing ten-triangle icon rather than a static F.

⚠️ **index's nav does NOT blend — its ink is painted.** Anything added to
its bar must take the page ink, not `#fff`: the mobile menu squares were
first shipped `#fff` (correct as a blend *source* on the other eight pages)
and rendered literally white on the homepage's light ground. They are
`--ink-footer` there now, flipping to `#fff` — along with the logo — only
while the dark menu overlay is open underneath them.

**The current page's link is inked `#fff`** — `.nav-links
a[aria-current="page"]{color:#fff}` — so it inverts to maximum contrast like
the logo, per the table above. That rule existed only on `contact.html` (and
in `handoff/theframeworks.css`, which was ahead of the pages) until the case
study round; it is now on every page that marks a current link. `index.html`
has no current link to mark.

The focus ring (`--f-red`) inverts along with everything else, so it changes
hue over different backdrops. It stays clearly visible, which is what the ring
is for.

**Nav links are 15px — the Details size — on all ten pages.** They went 14 →
18 → 15 over successive rounds; 15 is where they settled. Line-height stays
`1.2` and letter-spacing is `em` everywhere, including `index.html`, which
used to carry it as `.14px` — correct at 14, wrong the moment the size moved.
At 768px, the tightest width before the nav collapses to the mobile menu mark,
the link row is 373px with 155px of clearance from the logo.

### The page cap is 2200px

`--page-max` is **2200px**, set identically in the `:root` of all ten files.

⚠️ **It is mirrored in JavaScript.** `index.html` carries `const PAGE_MAX` for
`fit()`, which solves the hero's `--s` against `Math.min(innerWidth, PAGE_MAX)`
— raw `innerWidth` knows nothing about the cap and would size the hero for
space `.scene` doesn't have. Change the token and change the constant, or the
homepage hero quietly oversizes past the cap while every other page obeys it.
Verified after the move to 2200: at a 2600x2600 window `--s` resolves to
1.5278 (= 2200/1440), not the raw viewport's 1.8056.

Everything else derived from the cap follows on its own, which is the point of
having written them as ratios rather than pixel values — re-verified at a 2600
viewport: the Services logo wall's gaps and cells (`cqw`), the awards table's
alignment to the footer (0.00px drift on all four edges), About's EOA logo
(293.54px, ratio held), and the two full-bleed breakouts (still flush to the
real viewport edge, not the cap). No page raises a horizontal scrollbar.

⚠️ **Widening the cap makes two existing density problems worse**, both
already known and neither fixable in code:

- **About's team tiles** are now 477.5px. Mayuri Premdjee and Ross Sweetmore
  are 293px at source, so they render at **0.61x** — clearly soft. The rest of
  the set is 1.23x and Terry 1.34x.
- **The article cover** is 605px native against a 981px slot.
- The article's **text column** is now 805px, about 112 characters at 18px.

### Body copy runs at 1.3, not Figma's 1.2

The frame sets every named style at a 1.2 line-height. That is right for
headings and short labels and tight for running prose, so **the Body style
(18px) is set at 1.3 site-wide** while everything else keeps the frame's 1.2.

Scoped to the five places the Body style carries reading text:

| | |
|---|---|
| `article.html`, `article-2.html` | `.a-sec p` — the article prose |
| `services.html` | `.service p` |
| `about.html` | `.tm-name` |
| `thinking.html` | `.card h2` |

The 15px **Details** style (page intros, Thinking excerpts, awards rows,
About's "Challenge X to…" lines) and the 20px **H5** are deliberately still
at 1.2, as are all headings — they are different named styles, and loosening
a two-line label is not the same request as loosening a paragraph. If the
smaller reading text ever wants the same treatment it is a separate decision,
not an oversight.

`index.html` has no Body-style text at all — its copy is Details (15px) — so
it is untouched.

⚠️ **The articles' paragraph gap has to track the leading.** `.a-sec p + p`
is `margin-top:1.3em`: the frame separates paragraphs with an empty line, and
that margin reproduces it without an empty `<p>`. It is one line-height by
definition, so change one and change the other or the rhythm drifts.

### Keeping the nav smooth

Three things, all of which were wrong until Aug 2026 and which together
made the bar visibly stutter:

1. **The scroll handler is rAF-throttled.** Scroll events fire more often
   than the screen refreshes, so the class was being toggled several times
   per painted frame.
2. **The bar's height is measured once** (and on resize) rather than read as
   `navEl.offsetHeight` inside the handler — that read forced a synchronous
   layout on *every* scroll event.
3. **The direction threshold is 10px**, and the reference point only moves
   when the bar actually changes state. At the old flat 6px a trackpad's
   jitter could cross the threshold both ways in quick succession and the
   bar flickered up and down.

### The reveal — one entrance, site-wide

Everything that arrives on scroll, on every page, uses the same entrance:
objects **rise up into place**, and within a row **the leftmost goes first**.
The brief was "premium, smooth, Apple-like", and the difference between that
and merely "animated" is mostly duration — hence 2.2s, which is slow enough
that the move reads as a settle rather than a pop.

Direction and stagger order are two separate things here and it's worth being
precise about which is which: the *movement* is vertical (up), the *ordering*
is left-to-right across a row. An earlier revision had the movement itself
travelling left-to-right; that's what changed.

Four tokens, identical in every file's `:root`:

| Token | Value | Was |
|---|---|---|
| `--reveal-dur` | `2.2s` | `.8s`, then `1.1s` |
| `--reveal-shift` | `44px` (upward) | `28px` (and `24px` on Services) |
| `--reveal-stagger` | `.26s` | ad-hoc `.15s`/`.25s`, then `.13s` |
| easing | `--ease-out-expo` — `cubic-bezier(.16,1,.3,1)` | already site-wide |

The scroll reveal and the masthead load-in are deliberately twins —
`.js .reveal` (a transition) and `@keyframes reveal-in` (an animation) carry the
same distance, curve and duration, so the masthead and everything below it read
as one continuous idea rather than two systems that happen to share a page.
This replaced the old `rise-in`/`slide-in` keyframe pair, which travelled
vertically on five pages and horizontally on one.

`translate3d(0, …, 0)` rather than `translateY(…)` is load-bearing, not habit:
it puts the element on its own compositor layer for the whole move. At 2.2s a
non-composited transform is more than long enough for a dropped frame to show —
the longer and slower the move, the more compositing matters.

⚠️ **`--reveal-stagger` compounds and `--reveal-dur` doesn't.** A four-column
row waits `3 × stagger` before its last item even starts, so at `.26s` the last
card in a row begins 780ms in and finishes around 3s. If the cascade ever feels
drawn out, reach for the stagger first — halving it barely changes how any
single item moves, while halving the duration changes all of them.

**The stagger is per visual row, not per observer batch.** This is the one
genuinely subtle part. Arrivals are grouped by their top edge (`ROW_TOLERANCE`
40px), then ordered by their left edge, so the cascade always reads
left-to-right regardless of how many elements the IntersectionObserver reports
at once — and, critically, **each row restarts the count at zero**. The five
implementations this replaced all indexed the batch instead, which meant delay
kept accumulating down a long grid: fast-scroll the 21-card About page and the
last card would have sat still for nearly three seconds before appearing.
`entry.boundingClientRect` comes free with the entry, so the grouping costs no
extra layout work.

`REVEAL_STAGGER` in each script (260ms) mirrors `--reveal-stagger` in the
stylesheet. They're separate because one drives a `transition-delay` written
from JS and the other drives CSS `animation-delay` — change one and change the
other.

**Filter re-entry matches.** Work's and Thinking's filtered sets rise in on
the same `--reveal-dur`, so changing a filter reads as the same gesture as
scrolling something into view. Step-*out* stays short (300ms) and drops
*downward* — the opposite direction to the entrance, so the old set clears out
of the way rather than fighting the incoming one for the same path.

The incoming set is staggered by `staggerByRow()`, the same per-row grouping
the scroll reveal uses — **not** a flat index across the set. With 17 tiles a
flat index at the current 260ms stagger would leave the last card waiting over
four seconds before it started moving: acceptable for four cards arriving on
scroll, far too slow for something the user just clicked. Per row it caps at
780ms regardless of how many tiles match.

⚠️ **The rise is committed by an idempotent `commit()` with two triggers**: a
double `requestAnimationFrame` (the correct one — it waits for the
hidden→shown layout to land before the transition starts) *and* a 120ms
`setTimeout` fallback. rAF is paused in background tabs and in some embedded
viewers, and the incoming set starts at `opacity:0`, so with rAF alone a
filter clicked in a paused context leaves the grid **permanently blank**
rather than merely un-animated. This was observed for real: the preview pane
used to build this reports `rafFiredCount: 0`, and before the fallback every
filtered tile sat at opacity 0 indefinitely. Keep both triggers, and keep
`commit()` guarded — it will genuinely be called twice. Their cleanup timeouts were extended to `+1200ms` to outlast the
longer transition, or transient classes would be stripped mid-flight.

**`index.html` gained the `.js` guard** the other six pages already had —
`.reveal` is now scoped to `.js .reveal`, set by the script on first paint.
Without it, a blocked or broken script would leave every revealed element on
the homepage permanently invisible. It was the one page still exposed to that.

**What's deliberately exempt.** The logo ticker's constant drift and the About
carousel's drift/drag/inertia are continuous physical motion, not entrances —
an ease-out curve would make a steady scroll visibly lurch. The Services icon
build keeps its own `icon-build` keyframe (the square growing out from centre)
but now runs at `--reveal-dur` so it's coordinated with the card gliding in
beneath it. The awards table keeps a tighter 30–40ms row stagger: at the site-wide
260ms, 21 rows would take over five seconds to finish arriving.

### Full-bleed breakouts

Two elements deliberately ignore the 2200px page cap and run to the edges of
the viewport: the **logo ticker on the homepage** and the **B&W carousel on
About**. Both read as continuous bands rather than boxed-in elements, which is
the point of them.

```css
width:calc(100vw - var(--sbw));
margin-inline:calc(50% - 50vw + var(--sbw) / 2);
```

The `50%` resolves against the element's containing block — the capped, centred
page — and exactly cancels the auto margin the page uses to centre itself,
pulling the element flush to the viewport edges.

**`--sbw` is the part that isn't obvious.** `100vw` counts the scrollbar
gutter that `html{scrollbar-gutter:stable}` always reserves; the page's content
box doesn't. Without subtracting the difference, the breakout overhangs the
right edge by exactly the scrollbar width and raises a horizontal scrollbar.
It's invisible on macOS overlay scrollbars — which is why it survived an
earlier round unnoticed — and plainly wrong on Windows or with "always show
scrollbars" on. The script measures it once (`innerWidth −
documentElement.clientWidth`), re-measures on resize since the gutter moves
with zoom, and the token falls back to `0px` so a page without JS degrades to
the old naive behaviour rather than breaking.

Verified algebraically across scrollbar widths 0–17px at viewports 1280–3840:
the element lands flush at left 0 and its width equals `clientWidth` exactly in
every case. The zero-scrollbar case is also verified empirically; a classic
scrollbar can't be reproduced in the preview pane, which uses overlay
scrollbars.

These hold only while nothing padded sits between the element and `body`
(nothing does on either page) and no ancestor clips `overflow-x`.

### Other motion

Hover feedback runs `.3s`–`.5s` on the same `--ease-out-expo`. Nothing on the
site uses `cubic-bezier(.4,0,.2,1)` or a bare `ease` any more.

**Work** — filterable grid, rebuilt against the reworked frame (Aug 2026):
17 tiles, new imagery and captions throughout. The grid is **30 both ways**
now, 30px from the filter row, and rows are NOT uniform height — a span-2
tile is taller than a single, the row takes the tallest, and tiles
top-align (`align-items:start`) with the air below the short ones, as
drawn. Every media box is the same 3:2 at three spans (288 / 605 / 923 on
the 1440 basis), so the one `aspect-ratio` still carries all of them.

⚠️ **The caption is now the reworked frame's: client and title as one
two-line block.** Client 20px Regular in mid grey (18px on mobile) sitting
directly on the title — 20px Regular in Off Black `#1F1F1F` (`--ink-tile`
was repointed from the old `#29262A`) — then 10px down to the tags. The old
15px client and the 20/10/20 rhythm went with the old frame. One outlier:
the frame's Strategy Object tile still carries the old 15px client;
normalised to the 20px pattern, flagged in the notes. The full "Selected work" set keeps the frame's
editorial spans (now a 3-col UST hero and five 2-col wides); a filtered view
flattens to uniform tiles (`.is-filtered` on the grid) because the spans were
composed for that one set. Filter choreography: visible tiles step out downward with a small stagger,
the grid re-lays out, the new set rises in one by one. The active filter shows
a live count in red superscript — set via `position:relative;top:-.4em` on an
`inline-flex; align-items:baseline` button, not `vertical-align:super`, which
grew the line box and visibly pushed the label text down whenever the count
appeared. Project titles turn red on hover (`.tile:hover .tile-title`),
matching `.card-title` on the homepage.

**Imagery is real** (`assets/work/`, one JPEG per tile, ~1.2MB total). Each is
the composited export of that tile's *own media box* in Figma rather than the
underlying photograph, so overlays that sit on top of the artwork in the
design — the Level crop marks, the Durrell and Toshiba lockups, the G42 and
Price Forbes type — come through exactly as drawn instead of needing to be
rebuilt in CSS. They live inside `.tile-face`, which is the layer that scales
on hover, so the crop stays put while the image drifts within it.

⚠️ **`WellSaid` is still tagged only `Content`, which matches no filter
button** — unchanged in the reworked frame, so it remains reachable only
from "Selected work". The other off-filter word is now `Digital` (G42,
Strategy Object, Price Forbes, Siemens); all but G42 carry another indexed
tag, and G42 carries `Experiences`, so nothing else is orphaned.

⚠️ The frame's "Selected work" count is a hard-coded **18** again; there are
17 tiles. The built count is computed from the DOM, so it reads 17.

**Services** — ten cards on a fixed rhythm: **every title starts at 140px
from the card top and every description at 232px**, across all three rows.

That took undoing the original approach. The icon zone used to be
`flex:1 0 auto`, described as making "every title in a row sit on the same
line" — it did the opposite. Grid rows stretch every card to the tallest, so
a growing icon zone absorbs each card's *leftover* height and pushes its copy
to the card's **bottom**. A one-line title got a 193px icon zone against its
neighbour's 140, and one row's descriptions started at 254 / 232 / 254 / 254.
The zone is now a fixed **140** (Figma's own: a 100 mark over 40 of air), and
`.service h2` reserves two lines (`min-height:2.3em`, i.e. 2 x the 1.15
line-height, in `em` so it tracks `--fs-h4`).

⚠️ **Reversed on 2 Sep 2026 — the descriptions no longer share a line.**
The h2 used to carry `min-height:2.3em` to reserve two lines whatever the
title ran to, which was a deliberate departure from the frame (Figma lets
each description follow its own title — y=80 after a two-line title, y=49
after a one-line one). Myles reversed it: the cards should flow, with the
same 30px between a title and its own body, even though a one-line title
now starts its body higher than the two-line title beside it. Measured
after the change: a uniform 30px gap on all ten cards, and row two starting
at two different heights. The build matches the frame here now, and the
three-line-title constraint that came with the reservation is gone with it.

The row gap is **100px**, opened up from the frame's 60 on Myles' note that
the rows sat too close; 100 puts it on the page's own 100px rhythm. That one
is taste, not geometry — tune it freely.

#### The icons morph on rollover

Each mark now **toggles to a second state on rollover and stays there**,
morphing back only on the next rollover. It is a toggle, not a hover state —
roll off and it holds. Touch taps toggle it too. Ported from Myles' own icon
set (`icon-set-icon3-alt-no-rollover-colour.html`); none of the geometry was
re-derived here.

Ten icons, six techniques, because the two states are related differently in
each case:

| | icon | how it moves |
|---|---|---|
| `allRotate` | 1 | four diamonds rotate 45° and scale into their target squares at once |
| `slide` | 2, 5 | pieces each slide one grid unit / straight to their target |
| `diagonal` | 3 | a duplicate cluster travels up the diagonal and melts into the band (same fill, no seam) while the real square grows out of the shared corner |
| `xform` | 4, 7, 10 | pieces slide and/or scale about a fixed anchor |
| `anchorScale` | 6 | the two squares share a corner in each state, so each scales in place from it — nothing travels |
| `composite8` | 8 | static pieces + a translating square + one triangle whose vertices lerp |
| `composite9v3` | 9 | hero square drops; the rest swaps binary at `v=0.5`, the eased curve's peak velocity, so the cut is masked |

⚠️ **Icons 4, 7 and 10 no longer morph, and there is no third-party
library on the site any more.** They used Flubber. Two things were wrong
with that. First a real bug: `flubber.interpolate()` returns only **one
ring** for a multi-subpath path — measured, five rings in, one out — so all
three collapsed to a single square for the whole rollover and snapped back
at the end, which read as the icons vanishing on hover. Second, and fatal
even once that was fixed with `interpolateAll`: Flubber resamples every
edge into many points and eases them independently, so straight edges bow
and corners round off in flight. Against a set whose whole language is
hard-edged — a square slides, or grows from an anchor — it looked wrong.

They are rebuilt with the `xform` builder: per-piece translate and/or
non-uniform scale about a fixed anchor, `from:0` to grow a piece out of its
anchor. Each was derived from the two drawn states rather than invented —
icon 4's states are mirror images about x=90, so all five pieces are pure
horizontal slides; icon 7's bottom-right square travels one grid step and
lands **exactly** on the square that is static in both states, melting into
it the way icon 3's traveler melts into the band, while three others
stretch from a shared edge; icon 10 slides one, stretches three and grows a
fifth out of the corner the tall bar starts from. Verified: every piece
lands on its drawn state-2 geometry to within 0.6 units, and the worst
frame-to-frame area jump fell from 83–91% to 3–13%, in line with the
hand-built icons.

⚠️ **The marks are decorative and deliberately NOT focusable.** They carry no
information the adjacent copy doesn't already give, so they are `aria-hidden`
with no `tabindex`. The source demo made them focusable because there the
icon *was* the content; adding ten tab stops for an ornament would make the
page worse to keyboard through. Under `prefers-reduced-motion` the toggle
still works but swaps instantly, with no tween.

⚠️ **The rollover zone is the whole `.s-icon` box** (full column width ×
140px), not the 100px mark — the same zone the magnetic hover already used,
so the two respond to the same area. It means crossing the top of a card
triggers the morph. That is a one-line change (`.s-icon` → `.s-mark`) if it
ever feels too eager.

⚠️ **Every icon path is bled outward by a 1px non-scaling stroke in its own
fill colour** — `svg.s-mark path{stroke:var(--black); stroke-width:1;
vector-effect:non-scaling-stroke; stroke-linejoin:round}`. This is the same
fix the nav's logo mark uses and it is there for the same reason: each icon
is several separate `<path>`s, and two shapes meeting edge-to-edge each get
their own anti-aliasing pass, so the ground shows through as a faint
keyline down the join. Bleeding each shape makes neighbours overlap by a
full pixel while a free edge overhangs by half of one. `non-scaling-stroke`
pins that to SCREEN pixels, so it stays 1px at 100px, at 67px on mobile,
and mid-morph with a piece scaled 3x — in viewBox units it would grow with
the shape and visibly fatten it. `round` joins rather than miter: icon 8's
triangle has a 45° corner that would throw a spike.

⚠️ **`flubber.interpolate()` is the WRONG function here, and it is a silent
failure.** These icons are multi-*ring* paths — four or five separate
squares in one `d` — and `interpolate` only ever returns **one** ring:
measured, five rings in, one ring out. The endpoints looked perfect because
the code special-cases `v<=0` and `v>=1` to the raw state strings, so the
bug lived entirely in the frames between: all three icons collapsed to a
single small square for the whole rollover and snapped back at the end.
That was the "snapping" and the "disappearing on hover".

`interpolateAll` is the right call — one interpolator per ring. But it
demands two lists of **equal length**, and the design genuinely merges and
splits shapes: icon 7 goes 5 rings → 4, icon 10 goes 4 → 5. `padRings()`
pairs each ring with its nearest opposite number by centroid, then gives
whatever is left over a near-zero "speck" at the centroid of the ring it is
closest to — so an unpaired shape shrinks into its neighbour or grows out
of it instead of popping. Verified by stepping every icon through v=0→1 and
measuring rendered area at each step: the three morph icons used to swing
83–91% between frames and now move 6–13%, in line with the hand-built ones.

⚠️ **What the seam fix does and does not cover.** An instrumented pixel scan
(rasterise the live SVG, flag any light pixel flanked by fill) shows the
bleed doing real work once the morphs were fixed: stepped through the whole
rollover at the true 100px size, **icon 10 goes from 11 seam pixels to 2**,
icon 9 from 1 to 0 and icon 8 from 2 to 1. What survives is 1–2 isolated
pixels where two shapes meet **corner to corner** — icon 8's two triangles
at viewBox (150,90), and the hero square's corner at (90,90). Those are
point contacts in the drawn geometry, not anti-aliasing seams, and no
stroke bleed closes them; only overlapping the shapes at source would.

⚠️ **When measuring this, inline the styles onto the clone.** The scan
rasterises the SVG through a `data:` URL, and page CSS does **not** travel
with it — so `svg.s-mark path{fill;stroke}` is simply absent and every
shape renders as unstroked default black. An earlier pass concluded the
bleed "changed nothing" for exactly this reason: it was never in the
raster. Set `fill`/`stroke`/`vector-effect` as attributes on the clone.

`window.__tfIcons[n]` exposes each icon's `render(v)` so the morph can be
stepped frame by frame from the console — the preview pane freezes rAF, so
it is the only way to inspect the intermediate states where all of this
lives.

⚠️ **The SVG viewBox is `30 30 120 120`, not `0 0 180 180`.** Every mark is
drawn inside the frame's 30..150 grid, so the full 180 box carried a
30-unit margin on all four sides: at a 100px element only ~67px was ink,
inset ~17px from the left. That is why the icons read small and floated
away from the text. Cropping to the artwork makes the ink fill the box
exactly as Figma's own icon files do (theirs run 0..100 edge to edge) — the
mark is 1.5x bigger and **its left edge is the element's left edge**, so it
hard-aligns with the title and body beneath it. Measured: ink, title and
body all start at x=100 desktop and x=25 mobile.

⚠️ **`.s-mark` therefore carries no base `clip-path`.** It used to be
`inset(0 0 0 0)`, harmless while the viewBox had a margin. With the box
cropped it would slice icon 1, whose diamonds rotate through a bounding box
about 3 units wider than their start and end squares. The build-in keyframe
still animates `clip-path` and uses `backwards` fill, so the property
reverts to none once it finishes and nothing clips.

**`.s-mark` is whichever element carries the mark** — the `<img>` in the
markup, or the live `<svg>` the script swaps in for it. Both take the same
box and the same build-in, so the CSS never has to know which is there, and
a blocked script leaves the page exactly as it was before the feature
existed.

The ten icons are real SVGs (`assets/icons/`), downloaded from the frame. Each **builds from one small square at its own centre** on arrival:
`clip-path:inset(45% 45% 45% 45%)` at 0% leaves a small square in the middle,
relaxing to `inset(0)` by 100% — a literal "one square, then build out," not a
triangle morph (that was the previous design; replaced this round). Hover is a
separate concern on a separate property so the two can't collide: a small
JS-driven "magnetic" nudge translates the icon a few px toward the cursor as it
moves overhead (`±8px`, bound tight so it reads as a nudge not a drag) and eases
back to rest the instant the pointer leaves — "one square moves, then moves
back." Both use `backwards` fill on the load-in animation, not `forwards`:
after it ends the base `clip-path` applies, which is what leaves `clip-path`
free for anything that might need it later without a stale keyframe value
pinned in place. The logo wall is **all 30 marks** — see below. The awards table is sortable
by any column header — Level sorts by rank (Platinum → Shortlisted), Year ships
descending, rows cascade out/in on re-sort.

⚠️ **The awards heading sits 100px off its table, not the frame's 62.**
Figma draws 62px from the heading to the table header; Myles asked for 100
(2 Sep 2026) so it sits in the same air as the other section headings.
Mobile keeps 50 — half, on the mobile 25px grid — rather than 100, which
would swallow the viewport.

**The table is set to the footer's columns**, so the two read as one grid down
the page rather than two systems that happen to share a margin. The footer is
four flex children at `flex:1 1 0` with a 30px gap, so a footer column is
`F = (W - 90)/4` = `25% - 22.5px` of the content width both span. Project,
Awarding body and Category take one F each; Level and Year share the fourth,
which means `c4 + 30 + c5 = F` — Year gets a flat 45px and Level the rest,
`25% - 97.5px`:

```css
grid-template-columns:1fr 1fr 1fr calc(25% - 97.5px) 45px;
column-gap:30px;
```

The first three stay `1fr` rather than being written out: once the last two
tracks are fixed the leftover is exactly 3F, so they resolve to F on their own
and stay right if the cap or the inset ever moves. Measured 0.00px drift on
all four edges at 1200, 1440 and 2000. The 1100 and 767 overrides drop columns
and are independent of this — the footer reflows at those sizes too.

**The About carousel and the homepage ticker are two implementations of one
gesture, and they have to stay in step.** The strip felt worse to grab than
the ticker for three reasons, all of them things the ticker had and the strip
simply never got:

- **`dragstart` must be prevented.** Pull on a slide and the browser starts
  its own image drag — ghost thumbnail, pointer stream taken away mid-gesture.
  This was the big one.
- **`user-select:none`**, or the drag selects the page around it.
- **`touch-action:pan-y`**, or the browser arbitrates the gesture before the
  handlers ever see it. `pan-y` keeps vertical page scroll working over the
  strip.

The strip also now guards `e.pointerId` on move and release, so a second
pointer can't hijack a drag in progress.

One place it deliberately still differs: the ticker has no inertia, the strip
does (that's the designed "physical" feel — see "What's deliberately exempt").
Its release velocity used to be `vel = -dx * 60`, i.e. "px per frame, assuming
60fps". On a 120Hz pointer that halves every estimate and on a coalesced burst
it inflates it, so the same flick threw the strip a different distance each
time. It's now measured against `e.timeStamp` for real px/s, blended 0.7/0.3
so one twitchy last event before release can't decide the whole throw.

**About** — grey ground. 21 team cards with **real headshots**
(`assets/team/<first-last>.jpg`); they use the same site-wide reveal as
everything else now (this page's cards were the reference the unified
entrance was modelled on).

The headshots were mapped **per card**, not by export order. `get_metadata`
on `2896:11715` overflows its response limit, and `get_design_context` on it
overflows too — but the latter's overflow is *written to a file*, and that
file carries the whole JSX with `data-node-id` on every Team Member Card and
the name in the adjacent `<p>`. Parsing that file is what tied each image
constant to a person; a bare `download_assets` on the frame returns the raw
images **unlabeled** and caps at 20, and there are 21 people.

⚠️ **Two cards stack two images**, and the rule differs between them. Terry
Brissenden's card carries Mayuri's image as the component's base fill with
his own overriding it on top — there, the *last* image is correct. David
Alexander's two are the *same photograph at two resolutions* (585px and
320px), where the last is the worse one. Take the **larger** of a stacked
pair, and check any card that reports more than one image rather than
assuming the top layer wins.

⚠️ **Mayuri Premdjee and Ross Sweetmore are only 293px** at source, against
585px for everyone else (Terry is 640px). The tile is 287.5px at 1440 but
477.5px at the 2200 cap, so those two now render at **0.61x** — clearly soft
on a wide display (most of the set sits at 1.23x, Terry at 1.34x). This was chased down: `download_assets` returns the
*original uploaded* image for a node, and for both of them that original is
itself 293×293. Figma has no better pixels to give — the fix is to place a
larger image in the file, and nothing in code reaches it.

Each `<img>` carries its own true `width`/`height`, not a blanket 585 — they
differ per person, and the attributes are what the browser uses to reserve
the box before the JPEG lands. **The first row is `loading="eager"`**, the
other seventeen lazy: at 1440 the top row starts ~614px down, inside the
opening viewport, and lazy-loading an image that is already on screen just
delays it.

`alt` is empty on every headshot: each name sits in visible text directly
beneath its own photo, so a filled `alt` would have a screen reader announce
the same person twice. The EOA logo holds Figma's exact
182 x 76.632 shape via `aspect-ratio` and scales with the page — see below.
The B&W strip is **13 real photographs** (`assets/strip/`) in the frame's own
order and widths — see below. It's a wrap-around carousel: constant ~22px/s drift + pointer drag + inertia on
release, set duplicated once for the seamless wrap. It **breaks out of the
page cap** to run full-bleed — see "Full-bleed breakouts" above for the
formula and the scrollbar caveat. ⚠️ The frame's Terry Brissenden
card says "Challenge Ross to…" — corrected to Terry.

#### The header sits in equal air, optically

Services pads its header `calc(var(--nav-h) + 100px)` on top and, until this
round, a flat `100px` on the bottom. Both read 100 — and it looked wrong.

`--nav-h` (140px) is the nav's **box**, not its ink. The mark is `--logo-h`
(52.44px) tall and centred in that box, so it stops `(nav-h - logo-h)/2` =
43.8px short of the bottom edge. Measured from what you can actually see, the
headline had **143.8px of air above it and 100px below**. Figma has the same
asymmetry, and it isn't a mistake in the export: nav frame 140 tall with the
logo ending at y=90, headline cap at 240, icons at 460 — 150 above, 100 below.

The bottom now matches what the eye sees above:

```css
.page-head{
  --head-air:calc(100px + (var(--nav-h) - var(--logo-h)) / 2);
  padding:calc(var(--nav-h) + 100px) var(--pad-x) var(--head-air);
}
```

`--logo-h` is a new token, and `.logo` sizes itself from it, so the balance
re-solves on its own if either the bar or the mark changes rather than going
quietly stale. `--nav-h` is a `clamp()`, so this matters: measured 143.78 /
143.77 at a 1000px-tall viewport and 133.28 / 133.27 at 700px, where the clamp
pulls the bar down to 119px.

Two things make the measurement trustworthy. The headline is
`text-box:trim-both cap alphabetic`, so its box edges *are* its ink edges —
cap top and alphabetic baseline. And on mobile the pair being balanced is
different: the intro stacks under the headline there, so it is the intro's
bottom, not the headline's, that sits against the icons. The mobile rule uses
the same formula on its own 32px rhythm and lands 56 / 56 — which is exactly
the number that was previously hard-coded, so mobile renders identically and
merely stopped being a magic number.

⚠️ Worth knowing when measuring this sort of thing here: the masthead load-in
starts `--reveal-shift` (44px) low and holds it through `backwards` fill, and
animations freeze in the preview pane. A first measurement put the headline
44px too low — which is the shift value exactly, not a spacing bug. Settle or
disable the animation before trusting any masthead geometry. And disable
`animation`/`transition` only: a blanket `transform:none` also kills the nav's
centring `translateX(-50%)` and moves the logo you are measuring against.

⚠️ Every page measures its header padding from `--nav-h`, so all of them carry
the same 43.8px of invisible bar. Services is the only one where top and
bottom were *nominally equal* and so were expected to look equal; the others
set deliberately different bottom padding (Work 50, Thinking 60, Article 30,
About 0), so there is no symmetry there to break. Applying the same optical
treatment to them is a per-page design decision, not a bug fix.

#### The client logo rows

The 6x5 wall is gone (Aug 2026). The reworked frame runs the same **30
marks as two full-bleed rows** that drift like the homepage ticker — marks
01–15 above moving **left**, 16–30 below moving **right**, in the wall's own
order — under the "We've crafted meaningful work…" statement. Both rows can
be grabbed and scrubbed; drift resumes from wherever the drag leaves off.

- **Same implementation as `index.html`'s `.logos`**, instantiated per row
  with a `data-dir`: constant drift (suspended while dragging), pointer drag
  1:1, offset wrapped at one set's width, set cloned to cover any viewport.
  The three drag guards travel with it — `dragstart` preventDefault,
  `user-select:none`, `touch-action:pan-y`.
- **`ROW_SPEED` is 22px/s** against the homepage's 28 — "a nice slow pace"
  was the brief; the rows are a texture, not a carousel.
- The cell is the frame's own **182 x 78 with a 30px gap**; every mark is
  still the per-Listitem export (182 units wide, its own height), so the
  true relative sizes hold exactly as they did on the wall.
- **Mobile runs the marks at ~0.75 scale** — 136 x 58 cells, 22 apart, the
  two rows 75 apart — so about three show per phone width. ⚠️ Myles' call
  (28 Aug 2026), not the frame's: 3102:1644 draws the full 182 x 78 cells
  and 50 between rows. (A first 120 x 52 attempt read as tiny marks lost in
  air; 136 is the agreed middle.)
- Full-bleed uses the standard `--sbw` breakout (see "Full-bleed
  breakouts"); the token and its measurement were added to this page with
  the band.
- ⚠️ Myles' note asked for this change "on the About page" — the logo wall
  has only ever lived on Services, and that is where the updated frame
  draws the rows, so it was built here. The About frame carries no logo
  section. Flagged in the notes.


#### Services on mobile (frame `3102:1644`)

- **The cards run TWO-UP**, not stacked: 67px icons 20 over the 20px title,
  20 to the 16px description (the frame's own size — these are the
  narrowest columns on the site), columns 25 apart, rows 75. The desktop's
  fixed 140px icon zone and two-line h2 reservation are both released —
  the frame lets each description follow its own title here.
- **The awards regroup BY PROJECT.** The five-column table doesn't survive
  a phone; the frame turns it into project-name headers (20px) over one
  16px line per award — "Body, Category, Level" — with the year right-hung
  in mid grey and thin rules between. Rendered by the script from the same
  `AWARDS` array the table uses, so the two can never drift; the table
  hides ≤767 and the list ships in the table's default order (year, newest
  first). Sorting stays a desktop affordance.

#### The B&W strip

13 slides, `assets/strip/NN-name.jpg`, in Figma's order at Figma's widths
(507 / 380 / 380 / 507 / 212 / 507 / 285 / 475 / 285 / 285 / 304 / 380 / 507,
all 380 tall, 30px gap). The placeholder had 11 — two were missing.

**The widths live on `.strip-slide`, not on the `<img>`.** `measure()` reads
`track.scrollWidth / 2` to find the wrap point, and it runs before the
photographs have decoded; if the slide sized itself from its image the set
width would be measured as zero and the carousel would wrap instantly.

**The slides are Myles' own colour-graded exports, not the Figma renders.**
They arrived pre-cropped to each slide's exact aspect ratio at 3x (1140px =
380 x 3) and are resampled here to 2x. Because the ratios match to within a
rounding hair, `object-fit:cover` never actually crops — measured cropDelta 0
on eleven of thirteen and 0.0013 on the other two. It stays in place as
insurance against a future replacement whose ratio is off.

⚠️ **Don't re-grade them in code.** They read as black and white but are
stored as RGB (sampled chroma spread 0.28, max 1 — neutral), and the set they
replaced *was* desaturated here with a grey ICC profile. Running that over a
graded file would shift the tone the grade was chosen for. They're not
filtered in CSS either: the track drifts continuously and duplicates its set,
so `grayscale()` would have the compositor re-grading 26 large images every
frame for no change at all.

The responsive slide widths hold the ratios, so the tablet and mobile steps
crop no more than the desktop one: 400/300 and 293/220 are both within 0.002
of the 507/380 the artwork is cut to.

⚠️ Historical, and still true of the frame: the Figma sources are in colour —
Figma applies the black and white, and the section is named "People B&W" — so
a straight raw export gives you a colour strip.

⚠️ **Figma's codegen mislabels the crops.** Several slides come through the
design-context JSX as `object-bottom`. Following that hint drops the subject
clean out of frame — slide 3 renders as bare floor with the person cropped
off the top edge. Figma's own render of each node is centred; `object-fit:
cover` + `object-position:center` reproduces every one of the 13. Verified
slide by slide against the frame. Don't reinstate per-slide anchors from the
codegen without checking the node render first.

**Getting the images out was awkward and is worth writing down.**
`download_assets` on these nodes returns a usable 2× `export` for the first
four and then a **149-byte junk PNG** for the rest — persistently, not as a
transient rate-limit; retrying returns the same 149 bytes. `get_screenshot`
per node works reliably but only ever renders at the node's native size
(380px), so it can't give a 2× asset. What does work is `rawImages`, which
returns each photograph **twice** — a full-resolution original (up to
4032×3024) and a small copy. Take the larger, resize to cover 2× the slide
box, desaturate, encode. That's the pipeline that produced `assets/strip/`.

⚠️ Slide 13 is drawn in Figma as a 703px image **rotated 1°** inside a 507px
clip on a `#fff4f4` ground, and the earlier build reproduced it as a straight
centred crop without the tilt. That's moot now: the supplied file for that
slot (`Frame 1028950034`) is a different photograph from the one the frame
holds, so slide 13's content is Myles' choice rather than the frame's.

#### "Proudly employee owned" — cap the text, not the column

Figma splits this row into two equal **679** halves on its 1388 content area
with a 30px gap, and puts a **430-wide** block left-aligned at the top of the
right one. The build had `max-width:430px` on `.owned-body`.

That reads as the same thing and isn't. `.owned-body` is a `flex:1 1 0` item,
so clamping it to 430 doesn't leave the other 175px where it was — flexbox
redistributes the violation to the only other item on the row. The heading
column grew to **780px** and shoved the body from Figma's **51%** of the
content area across to **65%**, which is why it no longer lined up with the
HQ block underneath it (that one was right all along, and is the reason the
drift is visible at all).

The cap belongs on the paragraphs:

```css
.owned-body{ display:flex; flex-direction:column; gap:49px; }
.owned-body > p{ max-width:430px; }
```

Both halves go back to a true 1fr and the block sits where the frame draws
it. Measured at 1440: heading 605, body starting at 735 — **51.21%** of the
content area against Figma's 51.08%, the hair of difference being the fixed
30px gap sitting on a narrower content area. `.owned-body` and `.hq-address`
now start on the same 735 line. Verified at 2000 (equal 885 halves, both
columns at 1015), at the 1100 stack, and at 375.

**The general trap:** `max-width` on a flex item is not a local constraint. If
you want a column to hold its share of the row, cap what's inside it.

#### The EOA logo scales; it doesn't stretch

Figma draws the "Proudly employee owned" mark at **182 x 76.632** on the 1240
content area. It used to be pinned at a flat `width:182px`, so it stayed at
its 1440 size while everything around it grew toward the 2000 cap.

It now tracks the content area at Figma's own ratio:

```css
width:max(182px, calc((min(100vw - var(--sbw), var(--page-max)) - 2 * var(--pad-x)) * 0.14677));
height:auto; aspect-ratio:182 / 76.632;
```

Three parts, each load-bearing:

- **`aspect-ratio:182 / 76.632`** rather than leaning on the `width`/`height`
  attributes, which round the height to `77`. That rounding is invisible at
  182px and is not once the mark is half again as large.
- **`0.14677`** is `182/1240` — the mark's share of the content area in the
  frame. `min(…, --page-max)` is what stops it growing past the page cap.
- **`max(182px, …)`** floors it at Figma's size, so it only ever scales *up* —
  narrow viewports keep exactly the mark the frame draws.

`--sbw` is subtracted for the same reason the full-bleed breakouts subtract
it: `100vw` counts the scrollbar gutter and the content box doesn't.

Measured: **182.00 x 76.63 at 1440** (Figma exactly), **264.18 x 111.23 at
2000**, unchanged at 2400 (the cap holds), and floored at 182 on a 375px
phone. Ratio reads 2.375 at every width, and no case raises a horizontal
scrollbar.

**Thinking** — dark. Rebuilt (Aug 2026) as the reworked frame's **mosaic**:
**20 posts** on the 4-column grid (30 across, 58 down, `align-items:start`),
but cards now span **1, 2 or 3 columns** and every media box carries its own
aspect ratio — passed inline as `--ar`, so the markup owns each card's shape
and the page stays a template. Rows compose to 4 columns exactly (3+1,
1+1+2, 2+1+1 …), so auto-placement reproduces the frame's seven rows without
explicit placement. Titles moved from Body/Regular to **27px Light**
(`--fs-h4`, 21.6 mobile); wide cards cap their title at 493px and excerpt at
360px — the frame's own measures — so a two-column card doesn't set 750px
lines. On tablet the spans flatten to full-width; on mobile everything is
one column at its own ratio. Cover art re-exported per card
(`assets/thinking/`, 3.6MB, ~half photographic JPEG / half flat-art PNG).

Cover art is mostly illustration and typography rather than photography, and
several pieces are flat colour with hard edges. Those are kept as **PNG**
(they're 5–45KB each and JPEG rings on that kind of edge); the photographic
ones are JPEG. The rule in the export pass was a 64KB threshold on the PNG,
which sorted them correctly without having to judge each one.

Filters use the real byline categories — **AI 11, Culture 7, Strategy 2**.
⚠️ **"Creative" AND "Business" have no members** — the reworked content
dropped the Business posts — so both deal a random four (`pickFor` already
handled any empty filter generically; no code change was needed).

**Card 4 links to `article.html`** ("Your brand has got the answers…", the
Q artwork — the article's own cover) and **card 6 to `article-2.html`**
("I am challenging: Janelle"). Every other card is `#`.

⚠️ Copy calls on the reworked content (all flagged): **"cant" → "can't"**
and **"Why is pays" → "Why it pays"** corrected as typos; card 18's byline
category still reads **"Startegy"** in the frame and is corrected to
Strategy here. ("more that ever" was corrected the same way and has since
been fixed at source.) Two of the duplicates the first build reproduced
have also been resolved at source — card 7 is now "Are your brand
guidelines ready to deliver behaviour?" (and its media re-crops to
363x307) and card 17 is "Why it pays to play B2B?", which moves it to
Strategy. The remaining repeats are the frame's own: cards 10/14 share a
title, and the Alys Key excerpt appears on four cards.

**Contact** — dark, one viewport (`min-height:100dvh`, footer pushed to the
bottom). The frame shows the form *filled in* — those values became the ghost
placeholders. Submit stays hidden until every field has content, then rises
in; submitting swaps the form for a thank-you (no backend). The textarea grows
with its content. Top padding is 120px (doubled from the frame's 60px, and its
mobile override doubled to match) — the gap between the nav and the form.

⚠️ The dark frames paint some footer lines in Off Black on the Off Black
ground (invisible). The built pages keep the standard footer inked white.

## The case study page

`case-study.html`, rebuilt from Figma `3113:7185` (Case Study Collapsed) and
`3107:2283` (Case Study Expanded). **It is a template**: the masthead, the
intro + story copy, the details `<dl>` and the media stack all live in the
markup — a second case study is this file with different content, exactly as
`article-2.html` is to `article.html`. It uses the standard fixed semi-sticky
nav (it is a Work-section page, not a long read).

**Two routes lead to it**, and they use different markup for the same
whole-card click:

- **The homepage's "Case study / Botim" card** — `.card` is already an
  `<a>` wrapping its own image and meta, so it just took the `href`.
- **The Work grid's botim tile** — `.tile` is a `<figure>`, so it gets a
  stretched `<a class="tile-link">` absolutely positioned over the card.
  That is the one markup shape that keeps `figure > figcaption` valid with
  a whole-card link. ⚠️ The link is a *sibling* overlay, not an ancestor of
  the caption: a synthetic `click` dispatched straight at `.tile-title`
  will not navigate (it bypasses hit-testing), while a real pointer click
  there does. Worth knowing before concluding the link is broken — test
  with `document.elementFromPoint()`, which correctly reports `.tile-link`
  on top.

The other homepage cards and Work tiles still point at `#` — botim is the
only project with a page.

### The collapse — "Read the full story"

The one idea on the page. The story (Challenge / Insight / Solution) sits in
a grid wrapper that transitions `grid-template-rows: 0fr <-> 1fr`, so **no
heights are measured or hard-coded** — the fold stays correct however long
the copy gets, which is what makes the file a template. The read-link row
collapses by the same mechanism as the story expands, over the same duration
on the same curve, so the whole move reads as one continuous change of
height rather than two things happening.

- `--story-dur` is `.9s` — its own duration, on purpose: the fold is a
  change of state the user asked for, not an entrance. 2.2s would feel like
  the page ignoring the click, .3s like a pop.
- ⚠️ **The fold uses `--ease-fold` (`cubic-bezier(.4,0,.2,1)`), NOT the
  site's `--ease-out-expo`, and this is measured rather than taste.** Expo
  is severely front-loaded: over the story's 1337px it moves **149px in the
  first frame** — six times the linear rate — and then covers nothing at all
  for the last **267ms**. On a 44px entrance that front-loading reads as a
  confident settle; on a 1300px height change it reads as a lurch followed
  by a crawl, which is exactly what "choppy" was. `--ease-fold` peaks at
  **68px/frame** (2.7x linear) with a 50ms tail, so the fold moves at a
  near-even rate. Entrances everywhere else keep expo. **If you change the
  fold's distance or duration, re-check the per-frame step** — the curve is
  chosen against that number, not by eye.
- The copy fades *with* the fold, not behind it. It used to wait 35% of the
  duration before starting, so the box was open before the text arrived and
  the two read as separate events.
- The copy also fades, slightly behind the fold (delayed opacity), so it
  arrives as the space opens rather than sitting fully inked in a sliver.
- `visibility` flips at the transition's **ends** — delayed on the way out,
  immediate on the way in — which keeps the hidden copy out of the tab
  order and away from screen readers without a `display` jump.
- Both toggles are `<button>`s carrying `aria-expanded`/`aria-controls`;
  "Hide story" sits at the story's end, as the expanded frame draws it. On
  hide the page glides back up to the top block — without it the collapse
  yanks the media stack up under the cursor — and focus moves to the
  read-link so keyboard users aren't left inside the hidden region.
- ⚠️ **That glide is driven here, not by `scrollTo({behavior:"smooth"})`.**
  The native smooth scroll runs on its own curve for its own duration, and
  it was racing the fold's 900ms: two size-and-position animations
  disagreeing about where the page should be, frame by frame. It was the
  single biggest reason collapsing felt choppy. `glideScrollTo()` runs the
  scroll on exactly the fold's duration and curve — `foldEase` in the
  script mirrors `--ease-fold`, so **change one and change the other** —
  with the usual rAF-plus-timer fallback and a hard final assignment, since
  a half-finished scroll would strand the reader mid-document.
- **The mark animates.** A quarter-turn on hover (a plus reads the same at
  90°, so it spins without changing meaning), and on press the vertical bar
  collapses (`scaleY(0)`) so the plus becomes a minus as the read row folds
  away — the nav squares' morph language. Both are transforms; nothing lays
  out. The hide button's mark stays a static minus.
- **The mark is a `+` that becomes a `−`.** The frame draws it as a 13x13
  union of two 1px bars, 10px after the label (11x11 at 0.8px on the mobile
  template, so `.cs-pm` drops to 11px there). It is built from
  pseudo-elements rather than an SVG so it inherits `currentColor` and goes
  red with the label; the close state simply drops the vertical bar. Both
  toggles go **red on hover** (`--f-red`).

### The sticky details stop with the prose

The right-hand column (Type of work / Industry / Awards) is the article
pages' range-and-sticky mechanism with the roles swapped: the `<dl>` pins at
`--cover-stick` (100px) inside `.cs-aside`. Collapsed, the left column is
shorter than the details, so the pin has no travel; expanded, the details
follow the reader down the story. No `tuneSticky()` here — the details are
always shorter than any viewport, so the plain 100px anchor is always right.

**The details must never travel below the last line of the prose**, and
getting that right took two things, because a sticky element runs to the
bottom of its containing block and a grid item both *fills* and *feeds* its
row:

1. **The toggles live in their own grid row**, not in `.cs-copy`. The top
   block is `grid-row:1` = prose + details, `grid-row:2` = the toggles.
   With the buttons inside the prose column, `.cs-copy`'s box ended 73px
   below the last line (the "Hide story" row) and the details drifted that
   far past the text they belong to. The last story section also drops its
   trailing padding (`section:last-child{padding-bottom:0}`) so row 1 ends
   exactly on the text; the 50px down to the toggle is carried by
   `.cs-read`/`.cs-hide` instead.
2. ⚠️ **`contain:size` on `.cs-aside`**, which is the half that is easy to
   miss. Stretching alone is not enough — a grid item still *contributes*
   its content height to its row, and with the story collapsed the details
   (161px) are taller than the intro (117px), so they inflated row 1 by
   44px and pushed the toggle down with it: the 50px gap under the intro
   measured **94**. `contain:size` makes the element size as if it had no
   contents, so it takes the row's height without ever setting it. The
   details then overflow their own box whenever the prose is shorter than
   they are — which is what the frame draws, and nothing sits beside them
   in that column to collide with.

Both are structural, so the cap needs no measuring and no resize handler and
stays true however the copy or the type changes. Measured: overrun past the
last line of text is **0** at every scroll position, in both states, with
the 50px toggle gap holding either way.

⚠️ **The stacked layout (<900px) must re-place all three blocks.** The prose
and the details share row 1 on desktop; left as they were they land in the
same single-column cell and overlap. The mobile rules give explicit rows in
the frame's order — prose, toggle, details — set `contain:none` so the aside
takes its natural height in normal flow again, and carry the gap as a margin
on the aside (row gaps are 0 because the toggle brings its own 50px).

The details' gaps are the frame's own, read against cap-trimmed text: 32px
label ink to value ink, 50px between rows — deliberately larger than the
articles' meta (16/42), which is a different, denser block.

### The story rhythm

Set on the articles' `--body-line` system: paragraph break one line, module
break two (sections carry one line of padding each side), and the intro
into the first subhead is a full module break. Section subheads are the
articles' own style — **body size at Medium (500) in ink** — separating
themselves from the prose by weight, not scale. (The case-study frame drew
them mid-grey Regular with flat 30px gaps; Myles moved them onto the
article system on 28 Aug 2026, which settled it.)

### The media stack

Seven rows on the content area (not full-bleed), 30px apart: five
full-width singles and two 605/605 pairs. Ratios ride on each image's own
`width`/`height` attributes; the stack knows nothing about them — any mix
of `.cs-full` and `.cs-row` works. All of it uses the site reveal, staggered
left-to-right within a pair by the shared per-row observer.

⚠️ **The large Bo portrait that opened the frame's stack is out**, at Myles'
request (28 Aug 2026) — the faces grid now leads and carries
`loading="eager"`. `assets/casestudy/hero.svg` is still in the repo, unused,
so it goes back as a single `.cs-full` block if wanted.

Assets (`assets/casestudy/`, 2.0MB): the Bo hero and the faces grid are
**SVG** — the frame draws them as vectors, so they stay crisp at any width
(the hero is 3KB against a ~200KB raster). ⚠️ Figma's whole-node SVG export
bakes in two junk context rects (a grey backdrop and the page ground,
translated) — the committed files are the clean vector asset for the hero
and the export with those rects stripped for the faces. Everything else is
the composited 2x export of its own node, JPEG where photographic
(quality 82), PNG for the one flat-art tile under the site's 64KB PNG rule
(`bo-dark.png`, 37KB).

### Related projects

The Work grid's tile pattern (including the 20/10/20 caption rhythm — the
10 is Myles' call), two up, linking to `work.html`. The media ratio the
frame draws here (605:402) is the Work grid's own 3:2 to within a
hundredth, so the artwork is `assets/work/yokogawa.jpg` reused — the two
stay in step by construction. ⚠️ The frame draws the **same Yokogawa tile
twice**; reproduced as drawn, but it reads as placeholder content — flag
before a demo.

⚠️ One copy call made against the frame, flagged rather than silent: the
frame's masthead reads "Botim" with a capital B where the brand, the Work
tile and every line of the case study's own copy write "botim" — the build
uses lowercase.

(An earlier revision of this file claimed the desktop frames drew the
toggle as an arrow and only the mobile template used a "+". That was wrong
— `3119:8367` is a plus on the desktop collapsed frame too. The build now
draws the plus/minus at every width, as above.)

## The Brand Proximity page

`brand-proximity.html`, rebuilt on 3 Sep 2026 against Myles' own frame in
"The F website 2026" — `3437:2906` — after a first integration earlier the
same day from the other designer's separate "Brand-Proximity" file. That
hand-off package is still at `files/brand-proximity-handoff/` (outside the
site folder, never deploys) but the page no longer resembles it: the
layout, type, colours, overlays and the whole scroll model are this
frame's. Reached from **Services** ("Let's talk about your brand") and
article 1's inline mention; deliberately not a nav item, and it marks
Services as current the way `case-study.html` marks Work.

### How it reads

1. **Hero** (teal `#81C1C0`, normal flow). Headline in H2 top left and
   Mosaic 1 — the in-flow canvas that cycles three configurations on a
   4-second loop with a mouse-gravity hover — both starting 100px below
   the nav, as the frame draws them. The headline plays the site's
   masthead load-in.
2. **The stage** — one sticky screen holding four states, driven by the
   homepage's model. Scroll sets a target state; the drawn state chases it
   (`EASE_MAIN` 0.10); a stop snaps to the nearest whole state.
   - **0 Context** — the intro copy (H3, 82% of the content area) and the
     three stats, on the hero's teal, filling the screen. The copy reveals
     first, then the stats one by one on the site's stagger.
   - **1 Establish the supply** (`#CDE6E6`) slides up over Context
     carrying Mosaic 2 with it; heading, copy and sub-nav reveal once it
     locks.
   - **2 Understand the demand** (`#5B82E3`, white ink) slides up *under*
     the mosaic, which holds centre and morphs 2 → 3.
   - **3 Create AI-ready content** (`#F45944`, white ink) — same, 3 → 4.
3. **Release.** The runway runs out and the pin scrolls away with the
   page, red card and mosaic included. Nothing holds the view.
4. Contact module (H2, CTA in F Red), Related (two 605 squares), footer.

### The scroll model — the homepage's, on real scroll

⚠️ **The document genuinely scrolls.** `.bp-stage` is a runway whose
height is the Context screen plus `STEP × 3`; `.bp-pin` inside it is
`position:sticky`, viewport-tall and `overflow:hidden`. Every state is
`STEP` px of real scroll — **760 on desktop, the homepage's
`WHEEL_SENSITIVITY`**, so a wheel notch means the same thing on both
pages; 85% of the screen on a phone. The scrollbar stays truthful, browser
back/forward restores correctly, and a phone's native momentum scroll
works without hijacking touch — which is why this is a sticky runway and
not the homepage's `overflow:hidden` lock: that lock lives at scroll 0,
this experience sits mid-page.

- `vTarget = (scrollY − lockY) / STEP`, clamped 0..3, read on every scroll
  event. `vShown` chases it every frame. **Everything is drawn from
  `vShown`** — that single lag is the glide.
- Card *k* is translated down `(k − v)` screens, clamped 0..1, so it rises
  over the previous card as *v* runs *k−1 → k*. Cards are stacked by
  z-index in DOM order and pinned to the pin's **bottom** edge.
- **Snap**: after `SNAP_DELAY` (160ms) of quiet, resting between two
  states glides to the nearer one — the site's own glide
  (`cubic-bezier(.4,0,.2,1)` solved in JS, rAF + timer fallback, 600ms),
  ⚠️ never `scrollTo({behavior:"smooth"})`, and it cancels on any wheel,
  touch, key or pointer. Resting exactly on 0 or 3 never snaps, so leaving
  the stage in either direction is plain scrolling.
- The sub-nav buttons glide to `lockY + k × STEP`.
- Text reveals are driven from `vShown`: a card is `.in` once it has
  locked (`v ≥ k − 0.02`) and re-armed once it has slid most of the way
  back down (`v < k − 0.6`), so a second visit reveals again. The Context
  reveal is an IntersectionObserver (one-shot), like the rest of the site.

⚠️ **`lockY` is read from the stage, never the pin** — a sticky element's
rect reports where it is *stuck* (notes, trap 0d). It is the stage's flow
top plus `(ctxH − H)`.

⚠️ **The Context screen can be taller than the viewport** (any phone, and
a 720-tall laptop before the type step below). `measure()` then makes the
pin as tall as the copy and gives it a **negative sticky top** of
`H − ctxH`, so it sticks the moment its bottom edge meets the viewport's:
the reader scrolls the copy up, the stats arrive, and the screen locks
with the stats as its state-0 view. Where the copy fits, top is 0 and the
pin is the viewport — the plain case. `measure()` also writes the card
heights and the runway height in px, re-runs on resize and on
`document.fonts.ready` (the copy's height sets the pin's).

⚠️ **Under 760px tall (desktop), the Context copy and figures follow the
viewport height** — `min(var(--fs-h3), 4.2vh)` / `min(var(--fs-h2),
6.5vh)` — because at the frame's sizes the block measured 775px on a 720
screen and the pin would have answered by scrolling the copy's first line
up under the logo. At 900 the frame's sizes return. Related: browser
Geist wraps the copy at nine lines where Figma sets seven, so the block
is taller than the frame's even at 1440 × 900; the section pads
`--nav-h − 20px` at the top rather than the frame's 100 to absorb that.

### The mosaic under the cards

One `.bp-mosaic-stage` per card — the frame's art box, 840 × 960 units,
`--mosaic-w` wide — all three canvases drawn identically every frame (a
canvas paints above its card's ground and below its text only by being
that card's child). `measure()` places it at the frame's own spot:
**47.48% of the content area wide, starting 40.05% in, capped at 74.75% of
the viewport height, vertically centred** — 588.7 × 672.8 at 596.6 / 113.1
on 1440 × 900, the frame exactly.

- **Card 1's stage rides up with the card** — there is no mosaic beneath
  it. **Cards 2 and 3 counter-translate their stage** by the same amount
  the card moves, so the artwork holds the screen position of the one
  beneath while the card wipes up under it; the card's `overflow:hidden`
  clips the rising copy to the card, and since every canvas draws the
  same frame the seam is invisible. That is the whole "stays on top and
  morphs" effect, with no `position:fixed` anywhere — which matters
  because a transformed ancestor would break `fixed` anyway.
- **The morph clock** holds on Mosaic 2 while card 1 rises, then per leg
  holds for `MORPH_HOLD` (0.35) of the wipe and eases (`smoothstep`) to
  land exactly as the card fills the screen. Colour still hard-swaps per
  square, sweeping up from the bottom; positions are grid-snapped at
  render so squares hop cell to cell.
- ⚠️ **The frame draws Mosaics 3 and 4 with a larger cell than Mosaic 2**
  — 56.45 / 56.23 against 42.05 at 1440, i.e. **1.34×** — so `ZOOM`
  scales the art about the base box's centre along the same eased clock,
  and the canvas is 1.4× the stage on every side (`inset:-20%`) to hold
  it. Snapping is done relative to the zoomed grid's origin (the base
  centre is a whole cell corner in every state). Mobile holds one scale.
- ⚠️ **`MOSAIC_SQUARES` states 3 and 4 were re-derived from this frame.**
  State 2 matched the frame square for square (91/91, checked); the
  Understand mosaic is now 81 squares on a lighter blue ramp
  (`#4165BD / #5B82E3 / #7EA3FF …`) and the Create mosaic 80 on the red
  ramp, both centred in the 14 × 16 grid and shifted one column left so
  their centres land where the frame puts them (832 / 858 against
  Establish's 891 — one shared position, ⚠️ not three). Each of the 91
  squares was paired to a target by colour first then nearest cell, the
  surplus doubling up on their nearest target (drawn on top, invisible)
  rather than vanishing. Mean travel 2.2 cells on 2 → 3, 1.3 on 3 → 4.
  The derivation script is not in the repo; the inputs were the frame's
  `3438:6006` SVG and `3438:6264` groups + squares.
- Hover gravity is unchanged in kind; the three canvases share one screen
  position so whichever is topmost gets the events.

### The overlays

All in the stage's unit space (`--u` = one base unit), converted from the
frame's card coordinates, so they scale with the art at every size and
may hang outside it (several do). Card 1's three pop-ups **cycle one at a
time** (4s) while Mosaic 2 is the settled state, as the first build had
them; cards 2 and 3 show their three **together**, staggered by `--k`,
once the card has locked, and collapse the moment the state moves on.
Sizes: H5 (20) copy, H4 (27) or H3 (40) figures, 16px padding — all at
the frame's scale with px floors for small screens.

⚠️ **Three overlays carry the frame's own placeholder copy** — the dark
Insight card ("xxxxxx / xxxxx 142 …") and the "XX%" AEO card with its
lorem line — reproduced as drawn so the layout can be judged. Flagged in
the notes; Myles' to write.

⚠️ **Overlays are hidden on mobile** (`.bp-overlay{display:none}` ≤767):
at a phone's mosaic size they can't hold their copy and would sit over
the text bands. Flagged.

### The nav is fixed and painted here

At Myles' instruction: **no `mix-blend-mode`** — the ink is painted, as
`index.html`'s is — and **no hide-on-scroll**, so there is no `.is-hidden`
state and no scroll handler for the bar. Links are Off Black at 40%
(`rgba(31,31,31,.4)`, the frame's), hover and current full ink, the logo
and mobile squares `--ink-footer`, flipping to white only while the dark
menu overlay is open. ⚠️ Anything copied in from the eight blending pages
must swap its `#fff` blend sources for painted ink (notes, trap 0a).

### Type and layout, from the frame

- Card text: H4 heading (27 Light) 100 from the top, 226 wide (18.2% of
  the content area, so it grows with the cap), 30 down to the copy —
  a **SemiBold (600)** lead line, an empty line, then the body, all
  Details. 600 is loaded for this page only; the articles' subheads are
  Medium. Flagged as a call.
- Sub-nav: three Details lines 15 apart, bottom-left, 100 above the
  card's bottom; current full ink, others 50% on the sage card and 40%
  on the white-ink cards. Top and bottom offsets are `clamp(…, 11.1vh,
  100px)` so the block and the sub-nav can't meet on a short screen.
- Context: H3 copy on 82.3%; stats row 82.7% with `justify-content:
  space-between` on three ≤287.5 columns; figures H2, 24 to the body, 16
  to the mono credit (`#167170`, uppercase).
- Contact: H2 / 1.15, CTA in `--f-red`, padding `clamp(100px, 13.9vw,
  200px)` (200 at 1440, the frame's).
- Related: two 605 squares 30 apart, H4 Light titles on 493, the posts'
  own art and bylines (Charlotte's photo — the frame's unsplash source is
  that card's art — and the Q, which links to `article.html`).
- The hero's "Request your free sample report →" link is gone: the frame
  draws none, the closing module carries the CTA.

### Mobile (≤767)

The homepage's own mobile pattern: the sub-nav becomes a centred, wrapping
row under the permanent bar; each heading is placed under its own row by
`measure()` (the row wraps, so it is measured, ⚠️ off `offsetTop` — the
reveal holds the text 44px low until the card lands and a rect would read
that); the mosaic takes the band left between the heading and the copy,
which sits in a bottom band 40 up. Context is normal flow inside the pin
(0.8× type, stats stacked) and sticks by the negative-top rule above.

### Test hook

`window.__bp` — `frame()`, `measure()`, `snapNow()`, `readScroll()`,
`glideScrollTo()`, `fills()` (lock point, step, the four state
positions), and `shown` / `target` with **setters** so a state can be
forced. The preview pane freezes rAF and doesn't paint scrolled
positions, so the way to see a state there is: make the pin
`position:fixed; top:0` at scroll 0, set `__bp.shown = __bp.target = k`,
call `__bp.frame()` twice, then `document.getAnimations().forEach(a =>
a.cancel())` to land the frozen reveals. That is how every state above
was checked.

## The article pages

Two of them, on one template, rebuilt from Figma `2982:871` (article 1) and
`2990:2027` (article 2). They replaced a single earlier article page.

`thinking.html`'s first card opens article 1 and its second opens article 2 —
the headlines match those posts exactly. ⚠️ The Prompt card (12) used to link
to the old article page and is now inert again: that page is a different
piece now, and pointing a third headline at it would be wrong.

### The grid

Figma builds the page on a **12-column grid, 30px gutters**, inside the
standard 100px inset. Everything lands on it:

| | columns | at 1440 |
|---|---|---|
| text | 1 / span 5 | 499px |
| cover | 7 / span 6 | 605px (Figma draws 608) |
| second image | 7 / span 4 | 393px |

Written as a real 12-column grid rather than the old page's fixed percentages,
so all three scale together and stay on the same gutters. The text blocks are
**not** given explicit rows — they auto-place down column 1, so adding or
removing a section just works. Only the media is placed explicitly.

### The sticky handover

The one idea on the page, and the reason the grid is explicit.

Each `.a-media` is a **range, not an image**: an empty grid cell spanning the
rows its image should accompany. The image inside is `position:sticky`, so it
pins while that range is on screen and releases the moment the range scrolls
past. That is the whole handover — **no JavaScript**.

Article 1 spans the cover `1 / span 3` (masthead + the first two sections) and
the second image `4 / span 2` (the LEGO section onward). Article 2's single
cover spans `1 / span 6` — every row — so it pins for the whole read.

⚠️ **Span an explicit row COUNT, never `1 / -1`.** `-1` addresses the end of
the *explicit* grid, and these rows are all implicit (there is no
`grid-template-rows`), so `1 / -1` silently collapses to a single row. It cost
real time here: article 2's cover was trapped in row 1, which inflated that
row to the image's full height — pushing the body copy 424px down the page —
and left the range exactly as tall as the image, so there was no travel and
sticky never engaged at all. Both symptoms, one cause.

**The second image starts level with the body copy**, not with the subheading
of the section it belongs to, so it reads as sitting beside the prose rather
than heading it. The frame does this with an invisible duplicate of the
subheading pushing the image down; the build composes the same offset from the
values that produce it — `30px` section padding + `24px` one line of the
subheading + `30px` its margin = **84px**. Measured: image top and body copy
top both land on the same pixel. It also opens 84px between this image and the
cover as they pass, which is what stops the two reading as one column.

Measured on article 1 at 1440: the cover pins, unpins, and the second image
takes the pinned position in turn. **The stretch between those two is not a
void** — it is exactly the cover's own height, during which the cover is
sliding up and out while the second image follows it up the column. At scroll
1400 the cover occupies −207→398 and the second image 399→792: contiguous,
both on screen. The second image then takes the pinned position the first one
left. Sticky is scoped to its own containing block, so the first image is
genuinely gone rather than sitting behind the second.

⚠️ **The row span is passed as a custom property (`--row`), not as
`grid-row`.** This matters and it is easy to get wrong: an inline style beats
a stylesheet rule *whatever the media query*, so setting `grid-row` inline
kept the desktop rows on a phone and put the cover above the headline. The
markup sets `--row`, and only the `min-width:900px` rule turns it into
`grid-row`. The ranges also must not clip — an `overflow` other than visible
on an ancestor silently kills `position:sticky`.

### A square viewport for a portrait image

Article 2's cover is a portrait crop, and the page is otherwise built on the
square the cover column describes. It therefore sits inside a **square frame**
— `.a-frame`, the column's full width with `aspect-ratio:1/1` — with the image
capped to that height (`height:100%; width:auto`) and pushed to the frame's
right edge with `margin-left:auto`. Measured at 1440: a 605x605 frame holding
a 453x605 image, flush right, 152px of ground to its left.

**The frame is what pins, not the image** — hence `.a-stick` marking whatever
actually carries `position:sticky`, rather than the script assuming it is
always the `<img>`. The anchor maths then measures the square, which is the
box the reader perceives.

It also happens to retire the snap described below for this page: the square
is 605px, comfortably shorter than the viewport, so it anchors at the plain
100px. The tall-image handling stays for anything longer that arrives later.

Once stacked (<900px) the frame drops its aspect ratio and the image goes
full width at its natural proportions — the square only exists to hold a
portrait inside the desktop column.

### Tall images: scroll through, then anchor

`--cover-stick` (100px) is only the right anchor for an image **shorter than
the viewport**. A taller one — article 2's cover is 807px at 1440 — would pin
100px down with its bottom cut off below the fold, and because it engages
within ~50px of scroll it reads as an abrupt snap that never shows the whole
image. That was observed, measured, and is what prompted this.

`tuneSticky()` in each page's script refines every media image's anchor from
its real rendered height:

```
top = min(--cover-stick, viewportHeight − imageHeight − --cover-foot)
```

An image that fits anchors at 100px exactly as before. A longer one rides the
scroll 1:1 — sticky itself is what keeps that feeling locked, there is no
transition to lag behind the page — until its bottom edge has cleared into
view with `--cover-foot` (40px) of air under it, then locks, possibly at a
negative top. Measured at an 800px viewport: article 2's cover now travels
199px and settles at −47px with its bottom 40px above the fold, where before
it pinned after 52px with its bottom 107px below it.

CSS alone can't do this — a sticky `top` cannot reference the element's own
height — hence the measured pass, the same approach as `fit()` and `--sbw`.
It re-runs on resize and on each image's `load`. The images also now carry
their real `width`/`height` attributes, so the box is reserved (and
measurable) before the pixels arrive.

### The nav is not fixed here

It is ordinary content at the top of the flow and scrolls away with the page.
Every other page pins it, but a long read is the one place where a bar
reappearing on every upward scroll is a distraction rather than a convenience
— which is what the brief asked for. Nothing ever passes underneath it, so it
needs no background, no z-index and no script. It keeps the site's
`mix-blend-mode:difference` so the ink matches the other pages exactly.

### The masthead sizes to its content

No fixed height. The masthead is as tall as its headline and meta make it, so
the gap down to the first section is **the same 80px on every article** — 40px
of padding here plus 40px on `.a-sec` — whatever the headline runs to.
Measured ink-to-ink from the last meta value to the standfirst: **80.0 on
both**.

⚠️ **This reversed an earlier decision, and the two cannot both be had.** The
masthead was previously pinned to a fixed 425px so that both articles started
their body copy on the *same line*; the cost was that a shorter headline left
more air beneath it — 140px on article 2 against 83 on article 1. An even gap
and a shared start line are mutually exclusive the moment two headlines differ
in length. The even gap is what was chosen. Don't reinstate a height here
without knowing you are trading the rhythm back for a shared start line.

The meta labels and values are cap-trimmed, as the frame has them — that is
what makes the 16px and 42px gaps read as distances between ink rather than
between line boxes, and it is why the 80px above measures true.

### Type

**The headline is 50px** (`--fs-title`, clamped on the 1440 basis) at the
headline leading of 1.15 rather than the body's 1.3 — it is display type, not
reading type.

**Section subheads are body SIZE at Medium (500)**, not a larger H5. They
separate themselves from the prose by weight rather than scale, which is what
keeps a long read feeling editorial rather than chopped into headed blocks.
Geist 500 is in the font request at the top of each file; without it the
browser synthesises a fake bold and the distinction coarsens.

**The whole vertical rhythm is built from one unit: `--body-line`**, which is
`calc(var(--fs-body) * 1.3)` — a single line of body copy.

| | |
|---|---|
| paragraph break | **one** `--body-line` (the frame's blank line) |
| module break | **two** — a double line break |

So `.a-head`, `.a-sec` and (stacked) `.a-media` each carry one `--body-line`
of vertical padding, and wherever two of them meet the gap is two. Measured:
**23.4 / 46.8 at the desktop body size, 20.8 / 41.6 at the mobile 16px** —
the module break is exactly twice the paragraph break at both. That is the
point of deriving it from `--fs-body` rather than fixing it in px: the gaps
follow the type down at each breakpoint instead of holding a desktop measure,
which is what "update it across the breakpoints" needs to mean.

An earlier version used a flat 80px, which read as separated blocks rather
than one continuous article. Related still opens at 100px — it is not part of
the read, so a larger break there is deliberate. `.article` carries no bottom
padding of its own: a third value there only made that gap arbitrary.

⚠️ Figma is inconsistent on module padding — article 1's sections are `py-40`
and article 2's `py-30` — and neither matches this. The double-line-break
rhythm was the brief and it supersedes both.

The masthead-to-first-section gap is part of that same 80 — see "The masthead
sizes to its content" below for why it is no longer pinned to a height.

⚠️ **The frame's large body text is 27px (`--fs-h4`, Light), and it needs a
selector that can beat `.a-sec p`.** Both articles open with a 27px intro
paragraph, and article 2 sets its pull quote at the same size; a bare
`.a-standfirst` / `.a-quote` is specificity (0,1,0) against `.a-sec p`'s
(0,1,1), so the plain body rule won and both rendered at 18px — identical to
the copy around them, which is exactly the tell. They are scoped as
`.a-sec .a-standfirst` and `.a-sec .a-quote p` now. Keep a class on both
sides of the selector or this silently regresses.

The quote is Off Black with its attribution in mid grey, both at 27px, as the
frame draws it. **Its opening mark hangs** (Aug 2026): `hanging-punctuation:
first` where it exists (Safari), and a measured `text-indent:-.42em` on
`.a-sec .a-quote p` everywhere else — one quote-mark's width in Geist Light,
so the first letters of every line align on the measure. Scoped to the
quote; body copy never opens with a quote mark by design. The attribution sits **directly on the next line** — the frame
sets quote and credit as one block with no blank line between them, so its
`margin-top` is 0. (Amusingly the attribution was always right: it is a
`<footer>`, not a `<p>`, so nothing overrode it — the quote sat smaller than
its own credit.)

Otherwise straight from the frame's named styles, with one addition: the
article headline is **50px at 1440**, its own size between H3 (40) and H2 (60),
so it gets `--fs-title` clamped on the same 1440 basis and sits on the headline
leading of 1.15 rather than the body's 1.3. Everything else is the shared
scale. Letter-spacing is in `em`, as everywhere.

The frame separates paragraphs with an empty line rather than a margin; the
build uses `p + p { margin-top:var(--body-line) }` and real paragraphs instead
of empty `<p>`s — see the rhythm section above for that unit.

### Related articles

Two cards, top aligned, carrying the two different media ratios the frame
draws (one landscape, one portrait).

⚠️ **Two content mismatches in article 1's frame, corrected rather than
reproduced.** Its related tile 1 pairs the headline "Storytelling and
imagination in the age of AI" with the artwork belonging to a *different*
post (Rose's "live and let's be kind"), and gives the second card Sophie's
byline when that post is Ben's. Article 2's frame pairs the same headline with
the correct artwork, which is what settled it. Both cards use the artwork and
byline of the post they name, taken from `assets/thinking/`. Both link to
`thinking.html` rather than to the posts, which have no pages yet.

### Assets

`assets/article/` — 432KB total.

| | |
|---|---|
| `a1-cover.png` | The Q on its black ground (node 2982:896) — the reworked frame's cover, replacing the old pixel-grid SVG. |
| `a1-lego.jpg` | The second sticky image, re-exported from the reworked frame's own 393px crop at 2x. |
| `a2-cover.jpg` | Article 2's cover — now Janelle's "Change your Shoes" watercolour (node 2990:2183), 3:4, replacing the photograph. |

Related tiles on both articles now carry the reworked posts: article 1 pairs
the Charlotte square with "I am challenging: Janelle" — which links to
`article-2.html`, the first Related tile pointing at a real page; article 2
pairs the coffee cup with the Ross poster. ⚠️ Article 2's frame bylines the
Ross tile `24.03.26` where the post's own card says `26.02.26` — corrected
to the named post, per the standing Related rule.

## Architecture

### The scroll model

The single thing to understand: **`scrollDisplay` is the only state.** It runs
`-1` (full intro) → `0`–`4` (the five icon states). Every visual — tile
transforms, opacities, parallax, the sub-menu highlight, the nav mark — is
derived from it inside one `render()` rAF loop. Nothing owns its own state.

Input never sets it directly. Input sets `scrollTarget`; `scrollDisplay` chases
it each frame (`+= (target - display) * EASE_MAIN`). That single lag is what
makes it feel smooth, and it means wheel, touch, keyboard and clicks all share
one path.

**The document is genuinely locked while the experience runs** (`body`
`overflow:hidden`), not merely ignored by the handlers — otherwise the
scrollbar, or a browser restoring a scroll position, slides the page underneath
a running experience. `body.released` lifts the lock at Momentum and puts it
back on the way up.

⚠️ `render()` drives everything, so if it throws, the rAF chain breaks and the
whole page freezes — input included. `safeRender()` wraps it and releases the
loop flag so the next gesture can recover. Worth keeping.

### Layout: chrome vs. hero

Two independently positioned systems, which is what makes it responsive without
distorting the artwork:

- **Chrome** (nav, sub-menu, copy, project highlight) sits against the real
  viewport edges using Figma's own pixel offsets, via `clamp()`s that resolve to
  exactly those values at normal desktop sizes and only compress on small ones.
- **Hero** (`.hero`, a 1440×900 canvas) holds only the icon and headlines — the
  one piece whose *internal* geometry must stay proportional, because `KEYS`
  coordinates and headline offsets are relative to it. Scaled as a unit by
  `--s` and centred in the space left over.

`.hero` centres with `left/top:50%` + `translate(-50%,-50%)` rather than grid
centring — grid's overflow-centring is unreliable once the box is bigger than
its container in both axes and collapses to a top-left placement.

### The icon

Ten right-triangles, each half of a 200px cell. **`KEYS` is the source of
truth**: 10 tiles × 5 keyframes of `[col, row, rotationDeg]`. Edit that array if
the icon geometry changes.

- Grid step is `STEP = 100` (a *half* cell), because Empathy's frame is 800px
  wide and offset half a cell from the other four — a shared finer step lets one
  coordinate system address all five.
- Values were reverse-engineered from each state's exported SVG path data (three
  points → which cell, and which corner is *missing* → rotation), then rotations
  unwrapped to shortest-path so interpolation never spins further than it has
  to. It genuinely interpolates — it is not a sequence of flattened images,
  which is why it can be scrubbed mid-transition.
- `LOGO_KEYS` does the same job for the nav mark, with a sixth keyframe: the F.

**Seams:** each tile is its own SVG with its own anti-aliasing pass, so two
meeting edge-to-edge leave a faint light line. Each triangle is bled outwards by
a 1px `vector-effect: non-scaling-stroke` in the fill colour, which pins the
bleed to *screen* pixels — always exactly 0.5px, so neighbours overlap by a full
pixel (no seam) while a free edge overhangs by half a one (invisible).
Expressing the bleed in viewBox units does **not** work: it scales with the icon
and visibly overhangs when enlarged.

### The page below

- **Work grid** — Figma's alternating wide/narrow rows (712/393, 393/711,
  711/393 on the 1240 grid, 135px column gap, ~104px row gap). Cards lift in on
  an `IntersectionObserver`, left before right (`REVEAL_STAGGER`).
- **Logo ticker** — a marquee that runs on its own, and can be grabbed and
  scrubbed; releasing resumes it. Pointer events, so mouse and touch share a
  path.
- **Contact** — "Fancy a challenge? / Let's talk↗". The arrow is inline SVG
  drawn to match Figma (the `↗` glyph has a solid head; Figma's is a stroked
  diagonal with an open corner bracket) and steps right on hover/focus.

### Mobile (≤767px)

A layout reflow — the animation is identical.

- Desktop nav links are replaced by the menu mark — four 10px squares in a
  30px box. **The button opens the site menu now** (see "The mobile system"
  below); the old note about it being inert is history.
- The nav is permanent and the sub-menu sits in its own band beneath it.
- The nav mark holds the plain F; the morph is desktop-only (at 40px the states
  read as a smudge, and the nav is on screen the whole way down).
- Body copy and the project highlight move into a shared bottom band.

⚠️ The mobile `--nav-h`, `--hero-top` and `--bottom-band` values are
**deliberately duplicated** in `fit()` in JS, to keep the calculation
synchronous with paint. **Retune one and you must retune the other.**

## The mobile system (Aug 2026)

Rebuilt against the Figma frames labelled **Mobile** — the 375-wide page
templates plus `3142:9937` (mobile Nav Unselected) and `3142:9923` (mobile
Nav Selected). Everything below is duplicated per file, like the rest of the
shell.

**The type scale is 0.8 x desktop.** Measured off the Mobile frames three
independent times — Work's headline 60 → **48**, Services' 40 → **32**, the
case study masthead 40 → **32** — so it is a ratio, not a per-page choice.
The clamps' own minima (34 / 28 / 21) were never that ratio; they floored
far too small and are the main reason mobile read wrong. Each page now
pins its display tokens explicitly in the mobile `:root`.

⚠️ **The named text styles do NOT shrink.** Body stays **18** (the case
study mobile frame sets its prose at 18), Details stays **15** (Work's
mobile intro) and H5 stays **20** (Services' mobile card titles). They had
been dropped to 16 / 13 / 18, which was the other half of the same problem
— it made every page's supporting text a size smaller than drawn. The one
deliberate exception is Services' card description at **16**, which its own
frame draws that way in the narrowest column on the site.

⚠️ **An unbreakable string can outrun the 0.8 rule.** About's HQ email is a
single atomic token, so its width scales straight with the type size: at
the rule's 32px it measures 370px against a 325px column and pushed the
page sideways. `.hq-address` takes 24px on mobile instead — chosen so the
longest atomic string fits at 320px too. Check any block whose content
can't wrap before applying the ratio.

**Vertical rhythm is a 25px grid.** Anchored to the Work mobile frame,
which runs nav + **50** to the headline, **50** to the intro, **75** to the
filter row and **50** to the grid. Everything else was retuned onto the
same grid — the previous mix of 24 / 32 / 40 / 44 / 56 / 64 sat on no
system at all, which is what made the spacing feel arbitrary. Section
padding is 75, block separation 50, tight pairs 25.

**The refined bar.** At ≤767px every page except the homepage runs
`--nav-h:90px` and `--pad-x:25px` (they were clamps). The 40px logo sits in
a 90px bar with 25px insets, exactly as the Nav frames draw it.
⚠️ `index.html` keeps its own mobile geometry tokens: its `--nav-h` /
`--pad-x` are mirrored in `fit()` and retuning them means retuning the
script — see the homepage section. It gets the new button, menu and morph;
only its bar metrics stay as they were. A ≤9px inset difference against the
other pages, flagged as a judgement call.

**The button morph.** The mark is four 10px squares (30x30, replacing the
old 27px SVG), now built from four `<span>`s so it can animate: opening
fades the bottom pair out and stretches the top-left square across the top
row into the frame's 30x10 minus — reading as the left square sliding
across to cover the right one. Pure CSS off `body.menu-open`; ink is `#fff`
as a blend source like everything else in the bar.

⚠️ **The stretch is `transform:scaleX(3)`, not a width.** Width is a layout
property and the bar carries `mix-blend-mode:difference`, so animating it
re-laid out *and* re-blended the whole bar every frame — which is what made
the morph feel steppy. `transform-origin:left` makes the square grow across
to cover its neighbour rather than from its own centre.

**The menu** (`.mobile-menu`) is the Nav frames' full-screen overlay: a
dark ground under the bar carrying a 2-column grid of 1px-bordered square
cells — Work/Services, About/Thinking, then a diagonal-line cell beside
Contact — labels bottom-left at `clamp(24px,6.7vw,32px)` Light. Details
that matter:

- **The shared edges are single 1px lines**: every link cell carries a full
  border and the doubled edges collapse with -1px margins (`li:nth-child(2n)`
  / `li:nth-child(n+3)`). The diagonal cell has **no border of its own** —
  its right edge is Contact's border, its top edge is About's, and the
  diagonal and bottom line are two SVG lines at
  `vector-effect:non-scaling-stroke`.
- **Tapping a cell fills it F Red** (`.sel`, the Selected frame's state),
  then navigates 350ms later — instant under reduced motion.
- **The entrance is committed rAF+timer**, the same double-rAF-plus-120ms
  pattern as the filter grids, because the overlay flips from
  `display:none` and rAF alone is paused in background tabs and embedded
  panes (trap #2). Cells rise in top row first at `.55s` on a 60ms stagger
  — deliberately quicker than the site's 2.2s scroll entrance, because a
  menu has to answer the tap; the last cell lands at ~0.85s.
- The page behind is scroll-locked (`html{overflow:hidden}`), Escape and a
  resize past 767px both close it, and the button carries
  `aria-expanded`/`aria-controls`.
- ⚠️ **The articles' in-flow nav needed `position:relative; z-index:40`** —
  the overlay is fixed at z 30, and without a stacking context the bar (and
  its close button) would paint underneath it. The fixed navs already sat
  at z 40.

**Work on mobile**, from its template: the filter row is a single
non-wrapping line that **scrolls off the right edge** — it bleeds out of
the inset (`margin-inline:calc(-1 * var(--pad-x))`) and pads back in, so
the first button sits on the page margin while the trailing ones disappear
off the bezel; the scrollbar is hidden and the cut-off row is the
affordance. Tiles run single-column at the same 3:2, 30px apart, client
line at 18px.

## Tuning

| Constant | Value | Effect |
|---|---|---|
| `EASE_MAIN` | `0.10` | chase speed — the overall weight of the motion |
| `WHEEL_SENSITIVITY` | `760` | px of wheel travel per state |
| `TOUCH_SENSITIVITY` | `260` | px of finger drag per state |
| `FLICK_VELOCITY` | `0.25` | px/ms above which a short flick still advances a state |
| `SNAP_DELAY` | `160` | ms after the last wheel tick before snapping |
| `INTRO_GAP` / `_MOBILE` | `120` / `105` | px above and below the intro copy |
| `INTRO_SCALE_DESKTOP` | `1.5` | how much bigger the icon is during the intro |
| `LOGO_RETURN_VH` | `.22` | viewport fraction over which the mark unwinds to the F |
| `TICKER_SPEED` | `28` | px per second |
| `REVEAL_STAGGER` | `260` | ms between the left card and the right (mirrors `--reveal-stagger`) |
| `TILE_EASE` | array | per-tile lag; spread for more or less cascade |

**Snap-to-state:** once input stops, `scrollTarget` rounds to the nearest whole
state rather than resting on a fractional blend. Wheel debounces `SNAP_DELAY`;
touch resolves on `touchend`, where a fast flick commits a state even if the
drag was short.

`prefers-reduced-motion` is respected throughout.

## Assets

All local. Nothing points at Figma's asset CDN — those URLs expire about a week
after export, so everything was downloaded and re-pointed, oversized exports
resized to roughly 2× display size, and the two photographs converted to JPEG
(2.8MB → 376KB).

Empathy's and Momentum's project marks, the nav mark, and the contact arrow are
inline `<svg>` — no files.

**The homepage ticker now runs the Services treatment** (2 Sep 2026): the
same 182 x 78 cells 30px apart, the same 22px/s drift, and the same 30 SVG
marks from `assets/logos/`. It had been six low-resolution ~182×80 PNGs in
oversized `object-fit:contain` boxes — a leftover from the round where 22 of
the 30 supplied logo files exported as blank 1×1 pixels. The Figma home
frame draws one row of 30 at the same cell size as Services, so this closes
that gap and the two bands now read as one component. Mobile steps the cell
down to 136 x 58 at a 22px gap, as Services does.

⚠️ It stays **one row** here, where Services runs two in opposite
directions — that is what the home frame draws (`List`, 30 children). If it
should be two, it is the same change Services already documents.

## Known gaps

- **Copy and imagery are hard-coded**, one block per state and per card. The
  render code addresses them generically by `data-state`, so wiring a CMS means
  replacing the markup — the animation layer needs no changes.
- **Some links are inert** — work cards and the footer's FAQs/Legal/Cookies
  point at `#`. The nav is fully wired between pages, all "Let's talk" modules
  go to `contact.html`, and the footer's email is a real `mailto:`.
- **Headline type is a fixed size on a scaled canvas**, not fluid type. It has
  to stay locked to the icon's coordinate system, but very long headlines could
  overflow the hero on narrow viewports.
- **`KEYS` is the fragile part.** All five states are verified against Figma,
  but future icon changes should be made there and re-verified per state, not by
  swapping in flattened artwork.
