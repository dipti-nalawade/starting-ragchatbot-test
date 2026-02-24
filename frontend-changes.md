# Frontend Changes

## Dark / Light Theme Toggle

### Summary
Added a Dark/Light theme toggle button fixed at the top-right corner of the UI. Clicking the button switches between dark (default) and light themes. The user's preference is persisted in `localStorage` so it survives page refreshes.

---

### Files Modified

#### `frontend/style.css`
- Added **light theme CSS variables** under `body.light-theme` selector, overriding the default dark-theme `:root` variables.
- Added **`--theme-toggle-bg`, `--theme-toggle-border`, `--theme-toggle-color`** custom properties to both dark and light variable blocks so the button itself adapts to the active theme.
- Added **`.theme-toggle`** button styles: fixed position (`top: 1rem; right: 1rem; z-index: 1000`), pill shape, smooth hover/focus transitions, and a shadow matching the current theme.

#### `frontend/index.html`
- Added a `<button id="themeToggle" class="theme-toggle">` element immediately inside `<body>` (before `.container`), containing:
  - An SVG icon (`id="themeIcon"`) that shows a **sun** in dark mode (click to go light) and a **moon** in light mode (click to go dark).
  - A `<span id="themeLabel">` showing the target theme name ("Light" / "Dark").

#### `frontend/script.js`
- Added `themeToggle` to the DOM element declarations.
- Added **`initTheme()`** — reads saved theme from `localStorage` (defaults to `'dark'`) and applies it on page load.
- Added **`applyTheme(theme)`** — adds/removes `body.light-theme`, swaps the SVG icon between sun and moon paths, updates the label text, and saves the choice to `localStorage`.
- Added **`toggleTheme()`** — checks current theme and calls `applyTheme` with the opposite value.
- Registered `toggleTheme` as the click handler on `themeToggle` inside `setupEventListeners()`.
- Called `initTheme()` inside the `DOMContentLoaded` handler (before `createNewSession`).
