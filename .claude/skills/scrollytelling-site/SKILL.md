---
name: scrollytelling-site
description: >-
  Build bold, immersive, editorial "scrollytelling" websites through the Higgsfield
  website builder — a scroll-driven camera journey with a signature preloader/intro
  animation and a custom cursor, designed to take real creative risks instead of
  defaulting to a generic template. Use this whenever the user wants a site that should
  feel cinematic, immersive, high-craft, award-worthy, or "awwwards-style"; whenever they
  mention scrollytelling, scroll-driven storytelling, a scroll experience, a hero that
  plays as you scroll, an intro / preloader / loading animation, or a custom cursor; and
  whenever they ask to design a landing page, portfolio, agency, product, brand, launch, or
  event site that should stand out and NOT look like a stock template. Also use it for a
  "make me a website with Higgsfield" request that should be visually ambitious. It layers
  three always-on signature ingredients (a scrollytelling spine, a preloader with an intro
  animation, and a custom cursor) plus a risk-taking design ethos on top of the Higgsfield
  website pipeline. Do NOT use it for Higgsfield generation "apps" (image/video tools with
  Sign in with Higgsfield — those are type:"app"), for plain admin dashboards / CRUD tools
  where visual daring is unwanted, or for a simple copy/content edit to an existing site.
---

# Scrollytelling Site — bold, immersive websites via Higgsfield

## The bet

Most websites are generic because generating something safe is the path of least
resistance: a centered hero, a gradient blob, Inter everywhere, three feature cards, a
fade-up-on-scroll, done. It passes. Nobody remembers it.

This skill exists to break that reflex on purpose. You are making a site people screenshot
and send to a friend — a scroll-driven world with a curtain-raising intro and a cursor
that behaves like it belongs to *this* brand and no other. The goal is not decoration for
its own sake; it is **one committed idea, threaded everywhere, executed with real craft.**
Risk here means a *specific, defensible, coherent* choice — not randomness. Timid is the
only real failure mode.

## How this skill relates to the Higgsfield website builder

You do not hand-roll the stack. The Higgsfield website builder already owns the hard parts
— the React 19 + TanStack Start SSR Worker, the scroll-scrub camera journey, the asset
engine, the anti-generic design discipline (banned palettes, concept spine, reference
boards, the "wow" catalog), and the deploy. **That flow is the source of truth for HOW the
site is built. This skill decides WHAT to build and how far to push it.**

**First move, always:** call `get_website_creation_instructions` and follow that pipeline
end to end. When this skill and that flow touch the same thing, the flow's mechanics win —
its SSR rules, its full-page-screenshot gate, its palette bans, its deploy/publish gates.
This skill never overrides them. What it adds sits comfortably *inside* them:

- a strong default set of choices at intake (below),
- two ingredients that flow treats as optional or omits — a **preloader/intro** and an
  always-on **custom cursor**,
- a higher risk tolerance, with a concrete menu of moves.

Everything the preloader and cursor guidance asks for is written to *pass* that
mechanical gate, not trip it. That is the whole trick — see "Safety rails" below.

## Lock these choices into the Higgsfield flow

When the flow asks its intake questions, steer them like this (still *ask* the mandatory
Animation question — the user owns that call — just point the Recommended marker the right
way and explain why):

- **Type:** `website` (a standalone brand, no Higgsfield sign-in). If the request actually
  needs AI generation, accounts, or credits, it is a `type:"app"` instead — stop and
  switch flows; this skill does not apply.
- **Animation mode:** `animated-website` — the seam-locked scroll-scrub camera journey.
  This *is* the scrollytelling spine. Do not let a "simple landing page" framing talk you
  out of it.
- **Delivery tier:** `spectacle`. This matters — spectacle is the tier that already
  budgets for a **custom cursor** and a second WebGL/scrub beat, so choosing it makes the
  cursor a first-class citizen of the base flow instead of a bolt-on. Put an
  awwwards/immersive framing in the brief so the tier reads as intended.

Write these into `app/design-brief.md` at Phase 0 like the flow expects, and add one extra
brief block — **"Signature ingredients"** — naming the preloader concept and the cursor
concept and one sentence each on how they enact the concept spine. If they do not connect
to the spine, they are decoration; redesign them until they do.

## The three signature ingredients

These are the reason someone reaches for this skill instead of a plain build. They ship on
**every** build — always present, always reduced-motion- and touch-safe, and always
*married to the concept spine* (never three interchangeable stock widgets). What flexes is
HOW each one is expressed for this brand, never WHETHER it exists.

1. **Scrollytelling spine.** The scroll-scrub camera journey from the Higgsfield flow's
   `references/scroll-scrub.md`. Scroll *is* the timeline; the visitor flies the page
   through several connected generated scenes. The hero responds to input, never a passive
   autoplay loop. Build the journey as the page's structure in Phase 3, not an afterthought
   bolted on in Phase 4 — the base flow's gate catches "static page + camera journey added
   later," and so should you.

2. **Preloader with an intro animation.** The curtain-raise. It sets the tone in the first
   heartbeat and hands off into the scroll journey. The base flow does not include one — so
   this is your addition, and it is easy to do in a way that breaks SSR or the screenshot
   gate. Read **`references/preloader.md`** before building it: it carries the safety
   contract *and* a set of distinct intro concepts so you are not shipping the same generic
   spinner every time.

3. **Custom cursor.** A persistent signature that should read as a motif of the brand, not
   a laggy dot. Spectacle tier already expects one; this skill makes it non-optional and
   gives it depth. Read **`references/cursor.md`** — it covers the pointer/touch/reduced-
   motion contract (get this wrong and you break mobile and accessibility) and several
   cursor concepts to pick from.

## Take risks — the anti-generic ethos

The Higgsfield flow already bans the worst offenders (graphite+ember, AI purple glow, etc.)
and pushes concept spines and reference boards. This skill goes further: it asks you to
actively *choose the less obvious option that still works.*

The method, applied to every design axis (palette, type, layout system, motion signature,
cursor, preloader, section transitions, copy voice): generate three honest candidates,
throw away the first thing you thought of (it is almost always the template), and commit to
the boldest of the remaining two that you can still *defend in one sentence.* Coherence is
the safety net — a wild choice that threads the concept spine is craft; a wild choice that
doesn't is noise.

For the full playbook — the "generic tells" blacklist, the "reach for this instead" menu,
and worked examples of pushing an axis without losing the plot — read
**`references/risk-moves.md`**. Consult it at Phase 0 (concept) and again at Phase 1
(reference boards), which is where genericness is decided.

## Where each piece hooks into the pipeline

The Higgsfield flow runs in phases. Here is where this skill's additions land, so nothing
gets deferred to "later" and quietly dropped:

- **Intake:** steer Type / Animation / tier as above. Still ask the mandatory question.
- **Phase 0 (brief):** tier = spectacle; write the journey block (animated-website
  requires it) *and* the "Signature ingredients" block (preloader + cursor concepts tied to
  the spine). Run the risk-moves method on every locked choice here.
- **Phase 1 (boards):** design the intro/preloader moment and reflect the cursor motif in
  the boards. Re-roll any board that reads template-y — this is the cheapest place to fix
  generic.
- **Phase 2 (assets):** generate whatever the intro/cursor need (a logo/monogram for a mask
  reveal, a first-frame poster to hold under the preloader, a shape for the cursor motif)
  in the same async kit as the rest.
- **Phase 3 (build):** materialize the scroll-scrub spine as the page structure; mount the
  preloader overlay and the cursor component, both SSR-safe.
- **Phase 4 (motion):** wire the intro timeline, the cursor lerp/magnetics, and the
  scroll-scrub. One controller owns scroll→video time; don't double-drive it.
- **Phase 5 (gate):** run the base flow's mechanical checklist, plus the extra self-checks
  below.
- **Phase 6 (deploy):** deploy, then the cover/metadata and (only if asked) publish, per the
  flow.

## Safety rails — how the bold stuff stays shippable

A preloader and a custom cursor are exactly the two features that most often break an SSR
build or fail the full-page-screenshot gate. Hold this line and they won't:

- **SSR-safe.** No `window` / `document` / `navigator` at module top level or during render
  — init inside `useEffect` only, or guard with `typeof window !== "undefined"`. A
  top-level `window` reference crashes the whole site. This is the base flow's #1 recurring
  failure; the preloader and cursor are prime places to trip it.
- **The real page renders underneath.** The preloader is a *separate overlay layer*, not
  the page held at `opacity: 0`. Content beneath must be fully rendered in SSR so a headless
  full-page screenshot (the flow's only verification) shows the site, not a blank curtain.
  Never gate section content behind the preloader or an IntersectionObserver fade.
- **The preloader always self-dismisses.** Auto-remove on a max timeout (≈2.5–3.5s) even if
  a load event never fires, and remove it from the DOM / set `pointer-events:none` once done
  so it can't trap the page or the screenshot. Never gate dismissal on something that might
  not happen.
- **Progressive enhancement for the cursor.** The custom cursor is *additive* — the native
  cursor stays as the fallback. Enable it only for fine pointers
  (`matchMedia("(pointer: fine)")`); on touch/coarse devices do nothing and keep the system
  cursor. If JS fails, the user still has a working cursor.
- **Reduced motion is a real path, not an afterthought.** Everything is
  `prefers-reduced-motion`-gated with a static/instant fallback: the preloader dismisses
  near-instantly, the cursor drops its trailing lerp and snaps (or reverts to native), the
  scroll journey has its reduced-motion fallback from the base flow.
- **Performance.** Cursor and intro motion animate transform/opacity only, driven by
  `requestAnimationFrame` / motion values — never React state per mousemove.

## Definition of done — self-check before deploy

Run the Higgsfield mechanical gate first (that is mandatory), then confirm this skill's
own additions actually landed:

- The scroll journey is the page's spine, and the hero responds to scroll input (not a
  passive autoplay loop).
- A preloader with a real intro animation exists, ties to the concept spine, self-dismisses
  with a timeout failsafe, and leaves a clean full-page screenshot behind it.
- A custom cursor exists, is a coherent motif (not a stock dot), and is correctly disabled
  on touch and under reduced motion — with the native cursor intact as fallback.
- You can name, in one sentence each, the *distinct choice* made on palette, type, layout,
  and motion — and none of them is the first, safe, generic option.
- Nothing references `window` at module top level; nothing waits at `opacity: 0` for the
  viewport.

If any of those is soft, it is not done — tighten it before you deploy.
