Step 0 — Setup (15 min)
Create a minimal project: one folder with index.html, styles.css, and a README.md. No framework, no build tools — that's the point this week. Pick a real product to anchor it (a pair of headphones, an app, a chair — anything with a hero, features, and a signup/contact form). Having a concrete product makes the content decisions easier.

Step 1 — Semantic HTML skeleton first, no styling (45 min)
Build the whole page structure before touching CSS. The order forces you to think in document structure, not visual layout. Aim for this skeleton: a <header> with <nav>, a <main> containing the hero <section>, a features <section>, the form <section>, and a <footer>. One <h1> only, then <h2>s under it, never skipping levels. Open the page in the browser — it should be ugly but completely readable and logically ordered top to bottom.
Gate: Run Chrome DevTools → Elements, and confirm there's exactly one <main> and one <h1>, with no <div class="header">-style fake semantics.

Step 2 — The form with real validation messages (60 min)
Build a signup or contact form. Every input needs a <label for="..."> tied to an id. Use the right input types (type="email", type="tel") so you get browser validation for free. Then add visible, text-based error messages — not just red borders (color alone fails accessibility). Each error message gets id="email-error" and the input references it with aria-describedby="email-error". Mark required fields with aria-required="true".
Gate: Submit the form empty and confirm each error appears as readable text next to the right field.\

Step 3 — The aria-live region (30 min)
This is the headline accessibility requirement. Add a status region: <div aria-live="polite" aria-atomic="true" id="status"></div>. When the form submits successfully (or fails), write a message into it with a tiny bit of JavaScript (e.g. "Thanks, you're signed up"). A screen reader announces it without the user losing focus. This is the one place you'll write JS this week — keep it minimal.
Gate: Submit successfully and confirm the status text updates.

Step 4 — Keyboard navigation + focus styles (45 min)
Unplug your mouse mentally. Tab through the entire page. Every link, button, and input must be reachable, in a logical order, with a visible focus ring (contrast ratio 3:1 minimum). Don't remove the default outline unless you replace it with something equally visible. Add a "skip to main content" link as the first focusable element — a classic accessibility win that graders look for.
Gate: Complete the full page using only Tab, Shift+Tab, and Enter. If you ever lose track of where focus is, your focus styles aren't strong enough.

Step 5 — Style it (now, last) (60 min)
Only now add CSS to make it attractive. Mobile-first. Keep your focus states intact through styling — it's easy to accidentally kill them. Check color contrast as you pick colors (WebAIM Contrast Checker, 4.5:1 for body text).

Step 6 — Audit and fix (45 min)
Run both tools and fix what they flag:

Lighthouse (DevTools → Lighthouse → Accessibility) — target 95+
axe DevTools (browser extension) — target zero violations

These catch things like missing alt text, low contrast, and unlabeled inputs. Iterate until both are green.
Step 7 — README (30 min)
Document the accessibility features you implemented — semantic structure, the aria-live region, keyboard support, the skip link, contrast choices. This is what separates you from people who just "made it work." Include your Lighthouse score as a screenshot or note.

A realistic pace is 2–3 focused days. The non-obvious lesson this week: accessibility is structural, not cosmetic — that's why we build the HTML skeleton and test keyboard nav before styling.
Want me to scaffold the starting index.html for you to fill in, or would you rather build it from scratch and have me review it when you're done? The review path teaches more, but the scaffold gets you unstuck faster if HTML structure is still new.
