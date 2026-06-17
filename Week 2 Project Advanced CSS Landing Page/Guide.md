Step 0 — Carry over your Week 1 page (15 min). Start from your Week 1 HTML. You already have semantic structure and accessible focus states — don't rebuild them. This week is purely about the CSS layer on top. Copy the folder, keep index.html mostly as-is.
Step 1 — Set up your design tokens first (30 min). Before any layout, define your CSS custom properties in :root — colors, spacing scale, font sizes, transition durations. Then define the dark-mode overrides. Doing this first means theming and dark mode are nearly free later instead of a painful retrofit.
Step 2 — Mobile layout, 320px only (60 min). Resize your browser to 320px wide and build only for that. Everything stacks in a single column. Use Flexbox for the nav and any row-of-items. Don't write a single media query yet. This is the "mobile-first" discipline — if you start at desktop you'll fight it all week.
Step 3 — Scale up with min-width queries (60 min). Add breakpoints at 768px and 1200px, layering complexity upward. This is where Grid earns its place: the features section becomes a 2-then-3 column grid. Rule of thumb you're practicing: Flexbox for one-directional rows/columns, Grid for true 2D layouts.
Step 4 — Container queries on the cards (45 min). Make one component (a feature card) respond to its container's width, not the viewport. Wrap it in a container-type: inline-size parent and use @container. This is the newest skill on the list — a card that reflows based on where it's placed, not the screen size.
Step 5 — Dark mode toggle (45 min). Add a button that flips a data-theme="dark" attribute on <html>. Your tokens from Step 1 do all the work. Add a smooth transition on the color properties so the switch isn't jarring.
Step 6 — Animations, done right (60 min). Add entrance animations and hover transitions. Critical: only animate transform and opacity (GPU-accelerated, hits 60fps). Never animate width, height, margin, or box-shadow — they cause jank. Then wrap everything in a prefers-reduced-motion guard that disables it for users who need that.
Step 7 — Audit and ship (45 min). Open DevTools → Performance, record while scrolling/hovering, confirm you stay near 60fps (no red bars). Re-run Lighthouse to make sure you didn't break Week 1's accessibility. Then push to GitHub with a README documenting your token system and breakpoints.
Gate for each step: resize the browser through 320 → 768 → 1200 and confirm nothing overflows or breaks before moving on.

Now the design. Let me show you a target to reproduce:Here's a target design to reproduce. It's a clean SaaS-style landing page — swap in your own product. Study the structure, then rebuild it yourself in your own CSS (that's where the learning is — don't copy any code, there isn't any to copy):

------------------------------- CONTINUE ------------------------

That's your target. Now here's the design spec to go with it — this is what you'll define in Step 1 as your CSS custom properties, so you build the whole thing on a token system instead of scattering hardcoded values:
Color tokens (light → dark)
Define each as a variable in :root, then override in your [data-theme="dark"] block:

Page background: near-white #f7f6f3 → near-black #1a1a18
Surface / cards: white #ffffff → dark gray #26262420
Text primary: #1a1a18 → #f5f5f0
Text secondary (muted): #5f5e5a → #a8a8a0
Accent (the blue icon + badge): #185fa5 → a lighter #378add so it stays readable on dark
Borders: a translucent rgba(0,0,0,0.12) → rgba(255,255,255,0.14)

The trick: define semantic names (--bg, --surface, --text, --text-muted, --accent, --border), not color names. Then dark mode is just reassigning those six variables — the rest of your CSS never changes.
Type scale: hero headline ~28px (use clamp(1.5rem, 5vw, 2rem) so it shrinks on mobile), section headings 18px, body 15–16px at line-height: 1.6, small/caption 13px. Two weights only: 400 and 500.
Spacing: pick a scale and stick to it — 8 / 12 / 16 / 24 / 40px. Section vertical padding scales up at larger breakpoints.
Layout per breakpoint (your Step 2–3 work):

320px (mobile): everything single column. Nav links collapse to a hamburger or stack. Feature cards stack vertically. Form input and button stack.
768px (tablet): feature grid becomes 2 columns. Nav goes horizontal. Form input + button sit side by side.
1200px (desktop): feature grid becomes 3 columns (as shown), content max-width caps around 1100px and centers.

Notice the feature grid in the mockup uses repeat(auto-fit, minmax(160px, 1fr)) — that single line reflows 3→2→1 columns automatically as width shrinks, which is a clean way to hit all three breakpoints. That's your Grid usage. The Flexbox usage is the nav bar (logo pushed left, links pushed right via justify-content: space-between) and the side-by-side form row.
For the container query requirement (Step 4): wrap one feature card in a container-type: inline-size element and have it switch from a stacked icon-above-text layout to icon-beside-text when its own container passes ~280px — independent of the viewport.
One thing to carry forward from Week 1: keep your visible focus rings on the nav links, buttons, and the email input. It's easy to wipe them out when styling. Tab through before you ship.
Want me to review your token setup once you've drafted the :root block in Step 1? That's the highest-leverage place to catch problems early.
Opus 4.8 HighClaude is AI and can make mistakes. Please double-check responses.
