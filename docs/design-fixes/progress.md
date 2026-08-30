## Design Fix Progress Log
Last updated: 2026-08-30T13:33:00Z
Last updated by: Gemini 3.1 Pro (High)

### 1. AllTech article body alignment
Status: fixed
Root cause: .post-layout used a 220px 1fr grid even without a sidebar, pushing .post-content to the right. .post-content lacked margin auto for centering.
Files touched: layouts/_default/single.html
Notes: Added conditional `no-sidebar` class to collapse grid to 1fr when TOC absent, and `margin: 0 auto;` to `.post-content`. Verified via HTML structure on Guide and ECU pages.

### 2. Author profile alignment
Status: fixed
Root cause: .author-card was a full-width block in the wider .post-container, rather than constrained to the 680px width of the article body.
Files touched: static/css/design-system.css
Notes: Added `max-width: 680px; margin: var(--space-12) auto var(--space-8);` to constrain it to the body text width. Verified HTML/CSS.

### 3. Social icons distorted
Status: fixed
Root cause: SVG icons lacked flex-shrink: 0 and explicit width/height in CSS, allowing flexbox to distort them.
Files touched: static/css/design-system.css
Notes: Added explicit `width/height: 18px` and `flex-shrink: 0` to `.share-btn svg`.

### 4. Share icon styling
Status: fixed
Root cause: .share-buttons container lacked horizontal centering, making it unaligned with the constrained body text.
Files touched: static/css/design-system.css
Notes: Added `max-width: 680px; margin: var(--space-6) auto 0;` to center the block matching the article width. Added `cursor: pointer;` to button.

### 5. Light theme incomplete coverage
Status: fixed
Root cause: layouts/_default/single.html contained multiple hardcoded dark-theme hex colors (`#2a2a2a`, `#1e1e1e`, `#333`, `#888`) overriding the CSS variables, causing these components to remain dark when the light theme was activated.
Files touched: layouts/_default/single.html
Notes: Replaced hardcoded colors with `var(--color-bg-tertiary)`, `var(--color-text-secondary)`, `var(--color-border)`, etc. Checked `.post-toc`, `.reading-progress-bar`, `.author-card`, `.guide-item`, and `.share-buttons` - all properly use CSS custom variables.
Components fixed:
Components still broken (if budget ran out):
Notes:

### 6. General design polish (optional, lowest priority)
Status: fixed
Root cause: Author card social links were simple text rather than SVG logos. The third share button (copy link) had its SVG overwritten/hidden due to being a `<button>` element with browser styling quirks.
Files touched: layouts/_default/single.html, layouts/posts/single.html
Notes: Replaced author card social text links with inline SVG icons. Converted the copy link `<button>` in the share buttons block into an `<a>` element to guarantee consistent styling for its internal SVG. Verified visually across dark/light themes.
