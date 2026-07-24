# Custom cursor

A custom cursor is a *persistent* signature — it is on screen the entire visit, so it has
more chances to delight or annoy than almost any other element. Done well it is a motif of
the brand. Done badly it lags, hides the pointer on a phone, or strands a keyboard user.
This file gives the safety contract first (because the failure modes are real) and then a
menu of cursor concepts.

Spectacle tier in the base Higgsfield flow already budgets for a custom cursor; this skill
makes it non-optional and gives it depth. Build it to reinforce the concept spine — same
motif as the preloader where possible.

## The safety contract

1. **Fine pointer only.** Enable it exclusively when `matchMedia("(pointer: fine)").matches`.
   On touch / coarse pointers, do *nothing* — never hide the system cursor on a phone, never
   render a stuck dot. The custom cursor is a mouse-only enhancement.
2. **Progressive enhancement.** The native cursor is the fallback and must always work. The
   custom cursor is *additive*: if JS fails or hasn't hydrated, the user still has a real
   cursor. Gate the custom elements' visibility behind a JS-added class so SSR / no-JS /
   touch never shows a stray dot (and the screenshot stays clean).
3. **SSR-safe.** All browser globals inside `useEffect`. No top-level `window`.
4. **Reduced motion.** Under `prefers-reduced-motion: reduce`, drop the trailing lerp and
   snap the cursor to the pointer (factor 1) — or skip the custom cursor and keep native.
   Never ship a laggy trail to someone who asked for less motion.
5. **Keep affordances.** Hiding the native cursor with `cursor: none` is fine over general
   chrome, but keep the I-beam on text inputs/textareas and make sure the custom cursor is
   always *visible* against every background (contrast or `mix-blend-mode`). A user who
   can't find their pointer is lost.
6. **Performance.** Animate `transform` only, driven by `requestAnimationFrame` (or motion
   values) — never React state per `pointermove`. Use event delegation for context states,
   not a listener per element.

## SSR-safe skeleton (dot + trailing ring, contextual states, magnetic)

```tsx
// app/src/components/cursor/cursor.tsx
import { useEffect, useRef } from "react";

export function Cursor() {
  const dot = useRef<HTMLDivElement>(null);
  const ring = useRef<HTMLDivElement>(null);

  useEffect(() => {
    if (!matchMedia("(pointer: fine)").matches) return; // mouse only
    const reduce = matchMedia("(prefers-reduced-motion: reduce)").matches;
    const html = document.documentElement;
    html.classList.add("has-cursor"); // CSS reveals the elements + hides native

    let mx = innerWidth / 2, my = innerHeight / 2; // pointer target
    let rx = mx, ry = my;                          // ring, lerped toward target
    const onMove = (e: PointerEvent) => { mx = e.clientX; my = e.clientY; };
    window.addEventListener("pointermove", onMove, { passive: true });

    // Context state via delegation: put data-cursor="view|drag|play" on any element.
    const onOver = (e: PointerEvent) => {
      const hit = (e.target as Element).closest("[data-cursor]");
      html.dataset.cursor = hit?.getAttribute("data-cursor") ?? "";
    };
    window.addEventListener("pointerover", onOver, { passive: true });

    let raf = 0;
    const tick = () => {
      const k = reduce ? 1 : 0.18;                 // reduced-motion => snap
      rx += (mx - rx) * k; ry += (my - ry) * k;
      if (dot.current) dot.current.style.transform  = `translate3d(${mx}px,${my}px,0)`;
      if (ring.current) ring.current.style.transform = `translate3d(${rx}px,${ry}px,0)`;
      raf = requestAnimationFrame(tick);
    };
    raf = requestAnimationFrame(tick);

    return () => {
      cancelAnimationFrame(raf);
      window.removeEventListener("pointermove", onMove);
      window.removeEventListener("pointerover", onOver);
      html.classList.remove("has-cursor");
      html.dataset.cursor = "";
    };
  }, []);

  return (
    <>
      <div ref={ring} className="cursor-ring" aria-hidden="true" />
      <div ref={dot} className="cursor-dot" aria-hidden="true" />
    </>
  );
}
```

```css
/* Hidden by default — only the JS-added .has-cursor reveals them, so SSR/touch/no-JS are clean. */
.cursor-dot, .cursor-ring { position: fixed; top: 0; left: 0; pointer-events: none; z-index: 100;
  opacity: 0; will-change: transform; }
.has-cursor .cursor-dot, .has-cursor .cursor-ring { opacity: 1; }
.has-cursor, .has-cursor a, .has-cursor button { cursor: none; }
.has-cursor input, .has-cursor textarea, .has-cursor [contenteditable] { cursor: auto; } /* keep the caret */

.cursor-dot  { width: 6px;  height: 6px;  margin: -3px 0 0 -3px;  border-radius: 50%; background: var(--ink); }
.cursor-ring { width: 40px; height: 40px; margin: -20px 0 0 -20px; border: 1px solid var(--ink);
  border-radius: 50%; transition: width .2s ease, height .2s ease, border-color .2s ease; }

/* Contextual states, driven by [data-cursor] on <html> */
html[data-cursor="view"] .cursor-ring { width: 84px; height: 84px; }
html[data-cursor="drag"] .cursor-ring { width: 64px; height: 64px; border-style: dashed; }
html[data-cursor="play"] .cursor-ring { width: 72px; height: 72px; background: color-mix(in srgb, var(--ink) 12%, transparent); }
```

A label cursor ("VIEW", "DRAG", "PLAY →") is the same idea — render a `<span>` inside the
ring and swap its text from `data-cursor` instead of only resizing.

## Magnetic elements (the CTA pull)

Give primary CTAs a gravitational tug toward the pointer — a small, tactile signal that
makes buttons feel alive. Mark them `data-magnet` and lerp a fraction of the offset:

```tsx
// app/src/components/cursor/use-magnet.ts
import { useEffect } from "react";
export function useMagnet(ref: React.RefObject<HTMLElement>, strength = 0.3) {
  useEffect(() => {
    const el = ref.current;
    if (!el || !matchMedia("(pointer: fine)").matches) return;
    if (matchMedia("(prefers-reduced-motion: reduce)").matches) return; // no pull on reduced-motion
    const onMove = (e: PointerEvent) => {
      const r = el.getBoundingClientRect();
      const x = (e.clientX - (r.left + r.width / 2)) * strength;
      const y = (e.clientY - (r.top + r.height / 2)) * strength;
      el.style.transform = `translate3d(${x}px, ${y}px, 0)`;
    };
    const reset = () => { el.style.transform = "translate3d(0,0,0)"; };
    el.addEventListener("pointermove", onMove);
    el.addEventListener("pointerleave", reset);
    return () => { el.removeEventListener("pointermove", onMove); el.removeEventListener("pointerleave", reset); };
  }, [ref, strength]);
}
```

## Distinct cursor concepts — pick one that serves the spine

Don't default to a plain dot every time. Choose a motif and commit to it. But "serves the
spine" is not "wears a costume" — for some spines the most premium expression is *restraint*:
a clean difference-blend disc that is simply confident, where a themed, labelled pointer
would read as a gimmick. Coherence can live in tone and behavior, not a literal motif. Pick
the option that makes the site feel more *considered*, not busier:

1. **Dot + trailing ring** (skeleton above) — the versatile baseline; give it a *specific*
   contextual behavior (resize, label, blend) so it isn't generic.
2. **Blend-mode disc.** A single disc with `mix-blend-mode: difference` that inverts
   whatever it's over — reads as one confident graphic gesture. Great on high-contrast,
   monochrome, or editorial brands.
3. **Contextual label.** The cursor carries words — "VIEW", "DRAG", "PLAY →", "01 / 06" —
   that change by region. Turns the cursor into wayfinding. Fits gallery/portfolio/archive
   spines.
4. **Media-reactive.** The cursor scales up and softens over imagery/video, shrinks to a
   precise dot over text and controls — signalling "this is explorable" vs "this is
   readable."
5. **Motif cursor.** The cursor *is* the brand mark — the same monogram/shape used in the
   preloader mask and the section markers. The strongest option when you want one motif to
   thread the whole site.

## Self-check

- Disabled on touch/coarse pointers; native cursor untouched there.
- Elements hidden until the JS `.has-cursor` class is added (clean SSR/no-JS/screenshot).
- No top-level `window`; transform-only via rAF; delegation for context, not per-element
  listeners.
- Reduced motion snaps (or reverts to native); text inputs keep their caret.
- The cursor is always visible against every background, and it's a recognizable motif —
  not an anonymous dot.
