# Distinct choices — the anti-generic playbook

This is the "push harder" layer. The base Higgsfield flow already bans the worst palettes
and pushes a concept spine and reference boards — read and obey those. This file is about
what you do *on top* of that floor to make a site that is genuinely distinctive instead of
merely competent.

Read it at **Phase 0 (concept)** and again at **Phase 1 (reference boards)** — those two
phases are where genericness is won or lost. By Phase 3 the design is decided; you're only
implementing it.

## The core method: discard your first idea

For every design axis — palette, type, layout system, motion signature, cursor, preloader,
section transitions, copy voice — do this:

1. Generate three honest candidates.
2. **Throw away the first one.** It is almost always the template your training pulls you
   toward. The safe centered hero. Inter. The purple gradient. Three cards.
3. Commit to the boldest of the remaining two *that you can defend in one sentence.*

That last clause is the whole discipline. **Coherence is the license for risk.** A wild
choice that threads the concept spine is craft. The same wild choice with no reason behind
it is noise. If you can't say why it belongs to *this* brand, it's not bold — it's random,
and random reads as broken.

## Commit to ONE idea and thread it everywhere

The difference between "has some cool effects" and "is a designed thing" is a single
concept spine carried through every surface: the palette, the type, the motion, the
cursor, the preloader, the copy voice, and a recurring structural device. Pick a nameable
metaphor ("a calibration instrument", "an archive dossier", "a stage", "a field guide", "a
control room") and let it decide the details instead of deciding them one at a time.

## Generic tells — if you catch yourself reaching for these, stop

None of these is illegal in isolation, but together they *are* the generic template. Treat
each as a smell that you defaulted instead of chose:

- Centered hero over a gradient blob / aurora / mesh background.
- One "clean sans" (Inter/Helvetica/Geist) at default weights as the entire type system.
- Purple→blue "AI" gradient; or dark UI with a neon cyan/green accent.
- Three equal feature cards in a row with thin line icons.
- A grayscale "Trusted by" logo strip as the only visual texture on the page.
- Ghost/outline buttons whose only personality is a 200ms background fade.
- Fade-up-on-scroll as the *only* motion in the whole site.
- Every section a full-viewport `h-screen` block, stacked identically.
- A stock 3D blob / abstract render / isometric illustration doing the visual heavy lifting.
- Emoji standing in for a real icon set.
- Perfectly centered everything with characterless "clean" whitespace.
- Copy built from "Empower / Unlock / Seamless / Elevate / Delight", and em-dashes
  everywhere (the base flow bans em-dashes outright — respect that).

## Reach for these instead

- **Type.** A display face with actual character; extreme scale contrast (a huge headline
  against small precise labels); set something oversized, cropped, or overlapping the media;
  use a mono or an intentional serif with a written reason; hand-kern the hero. Type is the
  cheapest way to look expensive.
- **Color.** One disciplined palette with a *single* unexpected, fully-committed accent —
  not five. Let the generated imagery carry the richness and keep the UI restrained. Avoid
  the banned families; "bold" is not an excuse to reinvent AI-purple.
- **Layout.** Asymmetry. A broken or Swiss/editorial grid. An off-center hero. Content that
  overlaps or bleeds into the media rather than sitting politely beside it. A persistent
  structural element — a vertical rule, a running index, a ticker, a spine label.
- **Motion.** Motion *motivated* by the concept: a "calibration instrument" ticks and locks;
  an "archive" pages and stamps. Driven by the user's scroll/pointer, never a passive
  autoplay loop. One signature interaction, repeated as a motif, beats ten unrelated
  effects.
- **Cursor & preloader.** Make them motifs of the spine, not stock widgets — see
  `cursor.md` and `preloader.md`.
- **Copy.** A specific voice with a point of view and concrete nouns. Say the real thing.
  Cut the growth-deck filler. Zero em-dashes.
- **Structure.** A recurring device that threads the sections — a numbered chapter index, a
  running timecode, a spine label in the margin, a stamped section system. It turns a stack
  of sections into a single narrative.

## Worked example — one boring brief, three distinct routes

Brief: *"a landing page for a productivity app."* The generic route writes itself (centered
hero, purple gradient, three cards, fade-ups). Instead, pick a spine and let it cascade:

- **"Control room."** Palette: near-black + one signal-amber, restrained. Type: a technical
  mono paired with a tight grotesque. Layout: a persistent left status rail; content docks
  to a grid. Motion: readouts that lock as you scroll. Cursor: a precise reticle with a
  coordinate label. Preloader: an editorial counter booting the system to 100%.
- **"Field guide."** Palette: warm paper + ink + a single botanical green. Type: a humanist
  serif for headings, a clean grotesque for body. Layout: annotated diagrams, marginalia,
  numbered plates. Motion: pages turn / specimens are revealed. Cursor: a labeled magnifier.
  Preloader: a cover plate that lifts like a book opening.
- **"Stage."** Palette: deep theatre-red + warm white + brass. Type: a dramatic high-
  contrast display face. Layout: full-bleed acts separated by curtain wipes. Motion: the
  scroll raises and lowers curtains between scenes. Cursor: a soft spotlight. Preloader: the
  curtain rising on scene one.

Same product, three unmistakably different sites. That's the target — not "which effects do
I add," but "what is this thing, and what does that make every choice."

## Risk ≠ chaos — the guardrails

Bold still has to *work*. Keep all of this true while you push:

- **Legible and accessible.** Real contrast, visible focus states, keyboard operability,
  a genuine `prefers-reduced-motion` path. A cursor nobody can find or a headline nobody can
  read is a bug, not a risk.
- **Fast.** Transform/opacity animation, one owner per scroll timeline, SSR-safe.
- **On-floor.** The base flow's craft floor and palette bans still apply — don't "get bold"
  by resurrecting a banned family or dropping the reduced-motion fallback.
- **Coherent.** Every bold move serves the one spine. If it doesn't, it's the thing to cut,
  not the thing to keep.

Defer to the Higgsfield references for the specifics this file doesn't re-state: palette
bans and reach-fors (`design-recipe.md` / `reference-boards.md`), the reference-board
combinatorics (`reference-boards.md`), and the Tier-1 technique menu (`wow-catalog.md`).
This file is the nerve to actually *use* them boldly.
