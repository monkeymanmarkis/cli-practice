# Preloader + intro animation

The preloader is the curtain-raise. It owns the first heartbeat of the experience and hands
off into the scroll journey. Done well it earns attention before a single word is read.
Done carelessly it breaks SSR, traps the page, or fails the full-page screenshot the
Higgsfield platform takes. This file gives you both halves: a **safety contract** that keeps
it shippable, and a **menu of distinct intro concepts** so you never ship the same generic
spinner twice.

The base Higgsfield website flow does not include a preloader — this is your addition, so
you own getting it right.

## Non-negotiable: match it to the concept spine

A preloader that could be dropped onto any site is decoration. Yours should *be* the
concept. If the spine is "an archive dossier," the intro stamps and files. If it is "a
calibration instrument," a readout counts up and locks. If it is "a stage," the curtain
rises. Decide the metaphor first, then pick the mechanic below that serves it.

## The safety contract (get this wrong and the build fails)

1. **Render nothing on the server.** The preloader mounts client-side only. The SSR HTML
   ships the real, fully-visible page — so a headless full-page screenshot (the platform's
   only verification) shows the site, never a blank curtain. This also means the page is
   never held at `opacity: 0` waiting for the intro.
2. **SSR-safe.** Every browser global (`window`, `document`, `matchMedia`,
   `sessionStorage`) lives inside `useEffect`. A top-level reference crashes the whole site
   — the single most common build failure on this stack.
3. **Always self-dismiss, with a failsafe.** Drive the exit off a timeline `onComplete`
   *and* a hard `setTimeout` (≈2.5–3.5s max). If an asset stalls or the timeline hiccups,
   the failsafe still tears the curtain down. Never gate dismissal on a `load` event that
   may not fire.
4. **Clean teardown.** On finish, unmount the overlay (or `pointer-events: none` + fully
   faded). It must never sit on top of the live page trapping clicks or a later screenshot.
5. **Reduced motion is a real path.** Under `prefers-reduced-motion: reduce`, skip the
   curtain entirely (don't mount) or dismiss it near-instantly. No long animation.
6. **Play once per session.** Guard on `sessionStorage` so navigating around the site
   doesn't replay the intro every route change — and so it can't collide with a screenshot
   on every load.
7. **Don't hard-lock scroll unless you release it in the failsafe.** A short visual overlay
   with `pointer-events: none` is safest. If you *do* pause scroll, use `lenis.stop()` /
   `lenis.start()` and release it in *both* the completion handler and the failsafe/cleanup.

## SSR-safe skeleton (React 19 + TanStack Start, GSAP)

Mount it once near the root (e.g. in `__root.tsx`, after the page content). It renders
`null` until the client effect decides to show it.

```tsx
// app/src/components/preloader/preloader.tsx
import { useEffect, useRef, useState } from "react";
import { createPortal } from "react-dom";
import gsap from "gsap";

const MAX_MS = 3200; // hard failsafe — the curtain is always gone by now

export function Preloader() {
  const [mounted, setMounted] = useState(false); // client-only gate
  const [done, setDone] = useState(false);
  const rootRef = useRef<HTMLDivElement>(null);

  useEffect(() => {
    // Client only. Skip on replays and for reduced-motion users.
    if (sessionStorage.getItem("intro-played")) return;
    sessionStorage.setItem("intro-played", "1");
    if (matchMedia("(prefers-reduced-motion: reduce)").matches) return;
    setMounted(true);
  }, []);

  useEffect(() => {
    if (!mounted || !rootRef.current) return;
    let finished = false;
    const finish = () => {
      if (finished) return;
      finished = true;
      setDone(true);
      window.dispatchEvent(new CustomEvent("intro:done")); // seam → hero can enter
    };

    const ctx = gsap.context(() => {
      const tl = gsap.timeline({ onComplete: finish });
      // ↓↓↓ the chosen intro concept goes here (see below) ↓↓↓
      tl.to(".pl-panel", { yPercent: -100, stagger: 0.08, duration: 0.7, ease: "power4.inOut" });
    }, rootRef);

    const failsafe = window.setTimeout(finish, MAX_MS);
    return () => { window.clearTimeout(failsafe); ctx.revert(); };
  }, [mounted]);

  if (!mounted || done) return null;
  return createPortal(
    <div ref={rootRef} className="preloader" aria-hidden="true">
      {/* curtain panels / counter / masked logo — per the chosen concept */}
      <span className="pl-panel" /><span className="pl-panel" /><span className="pl-panel" />
    </div>,
    document.body,
  );
}
```

```css
/* app/src/styles.css (or a scoped file) */
.preloader { position: fixed; inset: 0; z-index: 90; pointer-events: none; overflow: hidden; }
.pl-panel { position: absolute; top: 0; height: 100%; width: calc(100% / 3); background: var(--paper);
  will-change: transform; }
.pl-panel:nth-child(1) { left: 0 } .pl-panel:nth-child(2) { left: calc(100% / 3) }
.pl-panel:nth-child(3) { left: calc(200% / 3) }
```

The seam matters: whatever the curtain reveals should be *exactly* the first scroll scene,
and the `intro:done` event lets the hero start its own entrance the instant the curtain
clears — so the intro and the journey read as one continuous move, not two.

**Avoid the double-open (animated-website only).** The scroll-scrub journey already has its
own opening beat — a poster-held first frame plus the hero's entrance. Bolt a preloader with
a separate reveal on top of that and the visitor gets *two* openings that fight each other.
Resolve it one of two ways, every time:

- **Use first-frame-hold (concept 5)** — the intro simply *is* the journey's opening beat,
  so there's only ever one open. This is the safest default on animated-website.
- **Or hold the journey's real scene-0 poster underneath your intro.** Whatever concept you
  pick (counter, curtain, mask), render the scroll-scrub's actual scene-0 poster as the
  layer directly beneath the preloader, and have the intro resolve *into that exact image*.
  The handoff is then one continuous picture, not a curtain that reveals a different frame
  which then re-animates.

Picking any other intro concept without doing one of these is the double-open trap — catch
it at Phase 0 when you name the preloader concept in the brief.

## Distinct intro concepts — pick one that serves the spine

Rotate through these; do not default to the same one every build. Each is one sentence of
mechanic + when it fits.

1. **Curtain / panel wipe.** 2–4 masked panels slide away (stagger) to reveal the first
   scene. Clean, fast, universal — good when the spine is "a stage/reveal" or when you want
   the intro to disappear into the journey.
2. **Editorial counter.** A real load percentage in oversized numerals, tied to actually
   preloading the heavy first assets (poster + first scroll-scrub leg), then a wipe. Fits
   "instrument/data/precision" spines. Cap it with the failsafe so a slow asset never hangs
   the count — clamp the number to 100 when the timeout fires.
3. **Type-set intro.** The brand name assembles — stagger in, mask-reveal, or kern into
   place — then *lifts into its nav position* via a FLIP move, so the wordmark you loaded
   with becomes the logo you browse with. Fits typographic/editorial brands.
4. **Logo / shape mask reveal.** The hero's first frame is revealed through an expanding
   `clip-path` monogram or motif shape. Pairs beautifully with a cursor built on the same
   shape — reuse the motif. Fits brand-forward, iconographic spines.
5. **First-frame hold.** Hold the scroll-scrub's frame 0 full-bleed; let UI and letters
   settle; surface a quiet "scroll" hint; hand off. The most seamless option with the
   animated-website journey because there is no separate curtain to reconcile — the intro
   *is* the journey's opening beat.

## Wiring the counter to a real preload (optional, concept 2)

If you use the counter, make it honest — preload the first scene so the journey starts
smooth, but never let a failed fetch strand the user:

```tsx
// inside the timeline effect, before starting the exit
const assets = ["/assets/scene-01-poster.webp", "/assets/scene-01a.mp4"];
let loaded = 0;
const bump = () => { loaded++; setPct(Math.round((loaded / assets.length) * 100)); };
assets.forEach((src) => {
  const el = src.endsWith(".mp4") ? document.createElement("video") : new Image();
  el.onload = el.oncanplaythrough = bump;
  el.onerror = bump; // errors still advance — never hang
  (el as HTMLImageElement | HTMLVideoElement).src = src;
});
// the MAX_MS failsafe still owns the ceiling; the counter is a nicety, not the gate
```

## Self-check

- Renders `null` in SSR; the page is fully visible without JS.
- No browser global at module top level.
- Exits on both `onComplete` and a `setTimeout` failsafe; unmounts cleanly.
- Reduced-motion skips it; `sessionStorage` prevents replays.
- The reveal seams into the first scroll scene, and `intro:done` cues the hero.
- The mechanic is recognizably *this brand's* — not a stock spinner.
