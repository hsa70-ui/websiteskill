---
name: harshs-website
description: Use when designing or building a website, portfolio or landing page that should stop people scrolling. Gives it one signature physical interaction with real physics, tactile detail, real thickness and life at rest, instead of fade-ins and hover cards.
---

# Harsh's Website

A studio playbook for websites that make people stop scrolling. It comes from taking apart the XLRI Prometheus Merch 2026 store (shop.xlri.ac.in/prometheus-merch-2026) line by line, from rebuilding it twice as a personal portfolio (a hanging rail, then a 3D conveyor), and from studying award-level interactive sites. Written by Harsh Agrawal. The aim is never to repeat the hanger rail. The aim is to repeat **the thinking that made it different**.

If the site is about a real person or company, collect their verified facts first (their own documents, their live site) and never invent a number to fill a label. Every object on the page carries a real proof number, so the facts matter more than usual.

---

## 1. Why Prometheus felt different

Most websites are a stack of rectangles: hero image, three feature cards, testimonial strip, footer. They move with fade-ins and hover lifts. Our own first two attempts at copying Prometheus were exactly this, a CSS carousel with hover transitions, and they were rejected as static, shabby and flat. Prometheus had these traits instead. Every new site should hit most of them.

1. **One physical metaphor taken from the subject's own world.** It is a merch store, so the products hang on a real clothing rail. The metaphor *is* the interface, not a decoration on top of it.
2. **Physics, not tweens.** Every piece is a damped spring and a pendulum, simulated every frame. Nothing animates from A to B on a timer.
3. **Alive at rest.** The rail drifts on its own at 26px/s and loops forever. A visitor who never touches anything still sees motion.
4. **Objects respond to each other.** Hover one and it turns to face you, lifts, and pushes its neighbours aside with a falloff of 1, 0.8, 0.48, 0.2.
5. **Real depth.** The rail is a parabola curving away in Z, projected through CSS perspective, so it reads as a sagging wire. Items sit turned on the rack at about -60 to -72 degrees, the way clothes actually hang.
6. **Tactile hardware details.** Chrome hook with a wooden bead, a price tag on a string rotated -8 degrees, a 3-stroke chrome tube (shadow, tube, shine). These small truths sell the illusion.
7. **Atmosphere behind, quiet around.** A four-corner pastel radial wash drifting over 26s, and a giant outlined brand word (text-stroke at about 8% ink) behind the scene. Everything else on the page is calm.
8. **The rest of the page echoes the hero object.** Product cards swap front and back views, combo cards overlap two or three product cutouts, and the bag counter does a spring bump (cubic-bezier .3,1.6,.5,1) when you add. A form error shakes. The metaphor keeps paying off below the fold.
9. **Built light.** One Next.js client component, a hand-written namespaced stylesheet, no animation library, pre-exported WebP images. The motion is maths, not a dependency.
10. **Respectful.** It honours prefers-reduced-motion, has a hidden keyboard list mirroring the rail, and a coarse-pointer mode where the centred piece always faces you.

**The one-line lesson:** pick the object people would touch in the real version of this thing, then make the page obey physics around it.

---

## 2. Process

Work in this order. Do not open a design system or template first.

### Step 1. Read the reference properly, if one is given
If the user points at a site to learn from, inspect what the browser already downloaded before guessing anything: response headers, framework fingerprints (`/_next/static`, `__next_f`), the page CSS (`@keyframes`, `transition:`, `transform:` with `var(--...)`), and the page chunk around `requestAnimationFrame` for constants. Write the constants down. Borrow mechanics only; never copy another site's brand, photos, logo or copy.

### Step 2. Choose the signature object
Ask: in the physical version of this subject, what would a person pick up, flick, pull, drag or open? Use the metaphor bank in section 3. Pick one. Write a single sentence: "The page is a ___ and the visitor ___ it."

### Step 3. Draw or source the objects
- Real cut-out product photos on transparent backgrounds are best (Prometheus used them).
- Otherwise hand-draw SVG objects with one consistent light direction (top-left), gradients for volume, and a transparent background so silhouette masks work. Check them on a contact sheet before building.
- Each object carries one **subject-true detail** (the LPG tanker had the real hazard plate "23 / 1075"; the teaching case showed its 58% breakeven chart).

### Step 4. Build the physics scene (section 5 has the code)
Ring or space, idle drift, springs for turn and lift, pendulum swing from acceleration, neighbour push, drag with fling, horizontal wheel, prev/next glide, coarse-pointer mode, reduced motion.

### Step 5. Give it thickness (section 6)
Flat cut-outs rotating in 3D look like cardboard. Stack darkened slices between a back plate and the face.

### Step 6. Atmosphere and type
Drifting wash, one giant outlined word, a small two-line kicker above the scene, a caption under it that names the hovered piece, a looping scrubber and two round buttons. Pair a characterful display face (wide or expanded weights work well for the outline word) with a quiet body face and a mono for numbers and tags.

### Step 7. Echo the object below the fold
Cards reuse the same objects, swinging gently, turning to face you on hover. Bundles overlap several objects. The detail sheet shows the object large, turning in. Counters bump. Errors shake.

### Step 8. Verify, do not assume (section 8)
Sample transforms twice with no input to prove it moves on its own. Hover and screenshot. Check phone width, dark mode, no horizontal overflow, no console errors, frame rate before and after heavy effects.

---

## 3. Metaphor bank (do not default to hangers)

| Subject | Signature object | What the visitor does | Physics to use |
|---|---|---|---|
| Logistics, supply chain | Conveyor belt of parcels | Scroll drives the belt; parcels tip and settle at the curve | Belt velocity from scroll, parcel tilt spring from acceleration |
| Logistics | Container yard stack | Drag a container; a crane hook lifts it with a cable | Rope or pendulum on the cable, stacking with gravity |
| Logistics | Route map | A truck drives the route as you scroll; stops pop open as it arrives | Path-following with eased speed, suspension bounce on stops |
| Healthcare | Weekly pill organiser | Flick lids open; each compartment holds a project | Hinge springs with overshoot |
| Healthcare | X-ray light box | Drag films onto the glowing box to read them | Drag with inertia, snap-to-slot spring |
| Healthcare | Stethoscope cable | The cable follows the cursor across sections | Verlet rope |
| Consulting, strategy | Deck of index cards | Throw cards off the top; they keep the angle and speed you threw them with | Momentum retention, lighter cards bounce less |
| Books, research, teaching | Bookshelf of spines | Pull a spine out; it rotates to show the cover | Spring pull-out, rotateY with thickness |
| Events, startups | Badge and lanyard wall | Hover a lanyard; the badge swings and flips | Pendulum plus flip spring |
| Startups | Launch pad | Scroll fuels the rocket; it lifts off at the section end | Scroll-scrubbed thrust with shake |
| Food, hospitality | Kitchen ticket rail | Orders slide along a steel rail and pin in place | Slide with friction, clip snap |
| Finance | Receipt printer | Scrolling prints the receipt line by line | Paper curl spring |
| Music, audio | Crate of vinyl | Flick through records; one slides out and spins | Flick inertia, spin decay |
| Personal portfolio | Desk of objects | Pick up and move items on a desk | Drag, gravity, collisions (Matter.js if many bodies) |
| Personal portfolio | Fridge with magnets and postcards | Rearrange postcards; magnets click into place | Snap spring, slight rotation on drop |

The hanging rail stays in the bank for clothing, merch and anything that genuinely hangs. Do not reuse it for unrelated subjects.

---

## 4. Reference sites and what to borrow

- **XLRI Prometheus Merch 2026** (shop.xlri.ac.in/prometheus-merch-2026). The full anatomy above. Borrow: rail engine constants, hook and tag hardware, wash plus outline word, combos that overlap objects, bump and shake feedback.
- **Bruno Simon** (bruno-simon.com, Awwwards Site of the Year 2020). The portfolio is a toy car you drive between projects. Borrow: let the title fall in and get bumped first so visitors learn things are movable; fake expensive effects (baked shadows, matcap lighting, blob shadows that fade as objects rise); put idle bodies to sleep; his car antenna is a spring reacting to opposite acceleration, the same trick as our pendulum swing.
- **Lusion** (lusion.co). Studio site with a playful real-time 3D scene and progressive reveal. Borrow: content revealed at a steady pace by the scene itself.
- **Igloo Inc** (igloo.inc, by Abeto with Bureaux). Webby 2026 winner for visual design aesthetic. Borrow: a single coherent world rather than sections.
- **Stripe Press** (press.stripe.com). Books shown as coloured spines on a dark shelf; opening one slides it into view in its own colour scheme. Borrow: each item owns a palette that takes over when opened.
- **Poolsuite** (poolsuite.net). The whole site is a fake 1990s operating system with a radio. Borrow: commit fully to the metaphor, down to release notes.
- **Ableton Learning Synths** (learningsynths.ableton.com). Teaches by direct manipulation; every drag is heard immediately. Borrow: explain by letting people play, not by paragraphs.
- **Teenage Engineering**. Product as hero on a plain ground, specifications laid out like engineering documents, one functional accent used only for actions and prices, tabular numerals. Borrow for the calm parts of the page.
- **Rauno Freiberg, "Invisible Details of Interaction Design"**. Thrown things keep the momentum and angle they were thrown with; lighter objects bounce less; give people landmarks to return to. Borrow for any drag or fling.
- **Pioneer, Corn Revolutionized** (Resn, Awwwards Site of the Year 2021). Scroll walks you through lab to field. Borrow: scroll as a physical journey through a process, useful for supply chain stories.
- **Awwwards inspiration collections on drag and physics** (awwwards.com/inspiration, search "drag", "physics"). Use for fresh examples before each new build.

---

## 5. Engine core (vanilla JS, no library)

This is the Prometheus rail generalised. Adapt the geometry for other metaphors; keep the spring and pendulum maths.

```js
const K = [1, .8, .48, .2];                       // neighbour push falloff
const clamp = (v, a, b) => Math.min(b, Math.max(a, v));
const mod = (a, n) => ((a % n) + n) % n;

function layout(w, h) {                           // desktop vs phone
  const s = w < 640;
  const hg = clamp(s ? Math.min(.42 * h, .76 * w) : .5 * h, 190, 440); // piece height
  const railY = h * (s ? .26 : .235);
  return { w, h, s, hg, u: hg / 400, gap: hg * (s ? .4 : .37), railY,
           persp: s ? 950 : 1350, depth: s ? 150 : Math.min(330, .17 * w),
           ox: w / 2, oy: railY - .28 * h, hook: 42 * hg / 400 };
}
// depth: a parabola away from the viewer; set stage perspective + perspective-origin (ox, oy)
const zAt = (c, x) => { const s = (x - c.ox) / c.ox; return -c.depth * Math.min(s * s, 4); };
// draw the rail as an SVG path by projecting the same points: k = persp / (persp - z)

function step(st, now, dt) {                      // dt in seconds, clamp to 1/30
  const c = st.c, ring = st.d * c.gap, m0 = c.ox - ring / 2;
  if (st.dragging) {}
  else if (st.glideTo !== null) {                 // prev/next buttons
    const e = st.glideTo - st.offset, mv = e * Math.min(1, 5.5 * dt);
    st.offset += mv; st.vel = mv / Math.max(dt, .001);
    if (Math.abs(e) < .4) { st.offset = st.glideTo; st.glideTo = null; st.vel = 0; }
  } else {                                        // idle drift 26px/s, paused on hover
    const paused = st.reduced || st.sheetOpen || (st.hovered !== null && !st.coarse);
    const rate = Math.abs(st.vel) > 39 ? 2.4 : 1.6;
    st.vel += ((paused ? 0 : 26) - st.vel) * Math.min(1, dt * rate);
    st.offset += st.vel * dt;
  }
  const b = []; for (let i = 0; i < st.d; i++) b[i] = mod(i * c.gap - st.offset - m0, ring) + m0;
  const hov = st.hovered;                         // from hitTest, or nearest centre on touch
  const j = hov === null ? 0 : Math.max(0, st.pw[hov] * .535 + .3 * c.gap - c.gap) + .12 * c.gap;
  const k = st.reduced ? 400 : 120, v = st.reduced ? 40 : 15;
  for (let i = 0; i < st.d; i++) {
    const t = st.motion[i];
    let l = 0;
    if (hov !== null && i !== hov) { const dn = Math.round((b[i] - b[hov]) / c.gap); l = Math.sign(dn) * j * (K[Math.abs(dn) - 1] || 0); }
    const X = b[i] + t.push;
    const view = 57.3 * Math.atan2(X - c.ox, c.persp - zAt(c, X));
    const target = i === hov ? -.8 * view : clamp(-56 - .5 * view, -80, -32); // stay below 90deg so text never mirrors
    t.yawV += (k * (target - t.yaw) - v * t.yawV) * dt;  t.yaw += t.yawV * dt;
    t.pushV += (140 * (l - t.push) - 21 * t.pushV) * dt; t.push += t.pushV * dt;
    t.liftV += (k * ((i === hov) - t.lift) - v * t.liftV) * dt; t.lift += t.liftV * dt;
    const mx = b[i] + t.push;                       // pendulum from horizontal acceleration
    if (isFinite(t.x) && Math.abs(mx - t.x) < ring / 2) { const vx = (mx - t.x) / dt; t.ax = .55 * t.ax + .45 * (vx - t.vx) / dt; t.vx = vx; } else { t.vx = 0; t.ax = 0; }
    t.x = mx;
    if (!st.reduced) {
      const len = c.hg * st.size[i] * .55, breeze = 40 * Math.sin(now / 1300 + 1.7 * i);
      t.swingV += (-38 * t.swing - 2.4 * t.swingV + clamp(t.ax / len * 31.5, -900, 900) + breeze) * dt;
      t.swing = clamp(t.swing + t.swingV * dt, -16, 16);
    }
    const el = st.els[i];
    el.style.transform = `translate3d(${mx}px,${c.railY}px,${zAt(c, mx)}px) rotateZ(${t.swing}deg)`;
    el.style.zIndex = i === hov ? 999 : 500 - Math.round(Math.abs(mx - c.ox) / 8);
    el.style.setProperty('--yaw', t.yaw + 'deg');
    el.style.setProperty('--lift', t.lift);
    el.style.setProperty('--shade', Math.abs(t.yaw) / 90);
  }
}
```

CSS contract: `.slot{position:absolute;width:0;height:0;transform-origin:0 0;transform-style:preserve-3d;will-change:transform}` and `.body{transform:translateX(-50%) rotateY(var(--yaw)) scale(calc(1 + var(--lift) * .07));transform-origin:50% 0;transform-style:preserve-3d}`. A `.shade` overlay masked by the object's own image, with opacity `var(--shade) * .85`, darkens pieces that are turned away.

Input rules:
- Hit-test with projected geometry, not DOM hover: narrow boxes for turned pieces, wide and sticky for the hovered one, so hover never flickers as a piece turns.
- Drag sets `offset = startOffset - dx`; on release `vel = clamp(fling, -1600, 1600)` and drift reclaims it.
- Horizontal wheel only (`|deltaX| > |deltaY|`), so vertical page scroll still works. Stage uses `touch-action: pan-y`.
- Centre offsets are `n * gap - ox`; prev and next round to the nearest and step one.
- On touch, the piece nearest the centre is always hovered; tap it to open, tap another to glide it to the centre.
- Mirror every piece in a visually hidden list of buttons; focusing one glides it to the centre.
- Pause the loop when the stage is off screen (IntersectionObserver) or the tab is hidden.
- On load, start with a high drift velocity (about 520) and a swing impulse per piece, so the rack slides in and settles.

---

## 6. Thickness, so it never feels like cardboard

```js
// p.tf = thickness as a fraction of piece height (truck .13, book .055, badge .016, felt .012)
function solidLayers(p, h, q) {                   // q: quality level 0, 1, 2
  const t = Math.max(1.5, p.tf * h * [1, .8, .5][q]);
  const n = Math.max(1, Math.min([10, 4, 2][q], Math.round(t / 2.4)));
  let html = `<img class="back" src="${p.srcBack}">`;        // darkest copy, carries the drop shadow
  for (let k = 1; k < n; k++) html += `<img class="edge" src="${p.srcEdge}" style="transform:translateZ(${-t / 2 + t * k / n}px)">`;
  return { html: html + `<img class="face" src="${p.src}">`, half: t / 2 };  // face at translateZ(+half)
}
```

- Make `srcEdge` and `srcBack` once by wrapping the SVG content in an `feComponentTransfer` filter with linear slopes of about .56 and .4. Do **not** use CSS masks or filters on every slice: masked slices dropped a test from 44fps to 4fps.
- Put the drop shadow on the back plate only, never on the face, or it smears across the edge.
- Centre the thickness on the hang point (face at +half, back at -half) so rotation pivots through the middle of the object.
- Add a self-tuning watch: average 60 frames after a 40-frame warm-up; if the mean frame time exceeds 25ms, drop one quality level and rebuild. Ignore frames longer than 250ms and hidden tabs.

---

## 7. Page anatomy and tokens

- **Hero:** full-height scene (about 90svh, clamped 580 to 940px), top bar overlaid (monogram or mark, name, one round dark action button), kicker of two lines above the scene, the scene, then caption, scrubber and two round buttons at the bottom.
- **Wash:** four radial gradients from the corners over the base colour, animated `translate3d(-2%,-1%) scale(1)` to `translate3d(2%,1.5%) scale(1.06)` over 26s, alternating.
- **Outline word:** display face, very heavy, expanded width, about 14.5vw (max 250px), transparent fill, 1.5px stroke at 7 to 9% ink, sitting near the bottom behind the scene.
- **Sections below:** eyebrow in small caps mono, a balanced two-line headline, a short lede, then pill tabs that filter a card grid. Cards reuse the hero objects with a gentle 4 to 5s sway and turn to face you on hover. Bundles overlap objects with a count badge.
- **Detail sheet:** bottom sheet on phones, centred dialog on desktop. The object hangs large on the left and turns in from -80 degrees; facts in a 2 by 2 grid of mono numbers; bullets below.
- **Feedback:** spring bump `cubic-bezier(.3,1.6,.5,1)` on counters and buttons, a 0.4s shake for invalid input, a toast that rises in.
- **Theme:** design both light and dark. Dark mode is a different time of day (for a depot, sodium-lamp amber at night), not an inverted palette. Physical objects keep their own colours in both themes.
- **Copy:** each object carries one proof number on its tag, the way a price tag carries a price. Plain, specific English in connected sentences, no em dashes, no buzzwords. Explain unfamiliar names on first use.

---

## 8. Verification before saying it is done

Run this with Playwright against the built page (wrap it in a doctype skeleton first):

```js
const a = await page.evaluate(() => [...document.querySelectorAll('.slot')].slice(0, 4).map(s => s.style.transform));
await page.waitForTimeout(900);
const b = await page.evaluate(() => [...document.querySelectorAll('.slot')].slice(0, 4).map(s => s.style.transform));
// every entry must differ: the scene moves on its own
const fps = await page.evaluate(() => new Promise(r => { let n = 0, t0 = performance.now(); (function f(){ n++; performance.now() - t0 < 3000 ? requestAnimationFrame(f) : r(n / 3); })(); }));
```

Also: screenshot desktop light, desktop dark and a 390px phone; hover the centre and screenshot; open the detail sheet; confirm `scrollWidth <= innerWidth`; collect `pageerror` and console errors; compare fps before and after any heavy effect (headless has no GPU, so judge the ratio, not the number). Look at the screenshots yourself before publishing.

---

## 9. Recipes from builds that shipped

### Box-shaped objects: use true CSS cuboids, not slices
Parcels, crates, books and devices are boxes. Build each as five faces (front, back, left, right, top) inside a `transform-style: preserve-3d` element with `backface-visibility: hidden`, sized by `--W`, `--H`, `--D`:

```css
.cube{position:absolute;left:calc(var(--W) * -.5);top:calc(var(--H) * -1);width:var(--W);height:var(--H);
  transform-style:preserve-3d;transform-origin:50% 100% 0;
  transform:translateY(calc(var(--lift) * var(--H) * -.32)) rotateZ(var(--tilt)) rotateY(var(--yaw))}
.f.front{transform:translateZ(calc(var(--D) / 2))}
.f.back{transform:rotateY(180deg) translateZ(calc(var(--D) / 2))}
.f.right{width:var(--D);left:calc((var(--W) - var(--D)) / 2);transform:rotateY(90deg) translateZ(calc(var(--W) / 2))}
.f.left{width:var(--D);left:calc((var(--W) - var(--D)) / 2);transform:rotateY(-90deg) translateZ(calc(var(--W) / 2))}
.f.top{height:var(--D);top:calc((var(--H) - var(--D)) / 2);transform:rotateX(90deg) translateZ(calc(var(--H) / 2))}
```
Real thickness for free, about six planes per object, and labels stay crisp HTML. Put tilt (rotateZ) before yaw (rotateY) in the transform list so the box tips in world space. Shade each face with an overlay (top lighter, sides darker) and print the subject on the faces: a waybill label with a barcode on the front, the object stamped on the side, tape on the top.

### A plane surface in perspective (belt, table, floor)
Project the surface's back edge and front edge with the same maths CSS uses, `k = persp / (persp - z)`, and fill between them in an SVG behind the 3D layer. Slats redrawn every frame at `mod(-offset, spacing)` make a belt visibly run. Keep `perspective-origin` well above the surface (about half the stage height) so the top surface reads.

### A scanner or gate as the focal point
Put a fixed device at the centre, such as an overhead scanner head on a gantry behind the belt. When an object's centre enters the zone, trigger a one-shot effect on that object (a laser line sweeping its label), increment a visible counter and caption it ("SCANNED · C03"). Idle drift becomes an event every few seconds.

### Scroll as a physical input
Let page scroll add velocity to the scene while it is on screen (`vel += scrollDelta * 9`, clamped) and let the drift spring pull it back. For a journey section, sample an SVG road with `getPointAtLength`, find the point at the viewport's 55% line, and let a vehicle follow it on a spring (stiffness about 36, damping 9) so it overshoots and settles at each stop. Swap the vehicle where the medium changes: a truck becomes a plane over water.

### Explain by letting people play
A small solver in the page beats a paragraph: a min-cost flow network where tapping a lane cycles normal, congested and closed while the plan re-solves, or a slider that walks across a breakeven. Label made-up inputs and illustrative curves as such on the page.

### Echo pieces
A split-flap board for headline numbers (cells cycle random characters, then land, with a quick scaleY flap); waybill or tag-styled cards that tilt toward the cursor; a detail view where the object's box opens its flaps and the object rises out on a spring.

---

## 10. Anti-patterns we have already paid for

- Shipping hover transitions and calling it motion. If nothing moves when the visitor does nothing, it is static.
- A generic CSS scroll-snap carousel standing in for a physics scene.
- Flat cut-outs rotated in 3D. Always add thickness.
- Guessing how a reference was built instead of reading its CSS and JS.
- Claiming which AI tool or agent built a site. Code shape is evidence of style, not proof of authorship.
- Pulling assets, photos or branding from the reference. Borrow mechanics only.
- Reaching for offensive-security or scraping toolkits to study a site. Inspecting a public page's own frontend files in the browser is enough.
- Letting kicker text sit on top of the scene. Leave clear air between the heading and the moving object.
- Long captions that truncate on phones. Shorten for narrow screens.
- Text on objects that mirrors when rotated past 90 degrees. Clamp the resting yaw.

---

## 11. Delivery

Build as one self-contained HTML page (inline CSS and JS, objects as SVG data URIs, fonts from Google Fonts only) unless the user asks for files in their own project. When it goes into a real project, port it to a single client component plus a namespaced stylesheet, the way Prometheus is built.