# Dark Mode Design

Date: 2026-08-30
Status: Approved

## Goal

Add dark mode to the Astro portfolio site: auto (system preference) by default, with a manual toggle in the header that cycles light → dark → system. No flash of wrong theme on load. User choice persists.

## Approach: Token redefinition

All colors already flow through semantic tokens (`--color-surface`, `--color-ink`, etc.) defined in `@theme` in `src/styles/global.css`. Tailwind v4 utilities compile to `var(--color-*)` references, so overriding those variables under a theme selector switches the whole site. Pages and components need no changes.

Rejected alternatives:

- Tailwind `dark:` variant everywhere — touches every file, colors drift out of one place.
- A dark-mode package — dependency for ~50 lines of code we already own.

## Dark palette (soft gray-blue)

| Token | Light | Dark |
|---|---|---|
| `--color-surface` | `#ffffff` | `#151a23` |
| `--color-muted` | `#f9fafb` | `#1c222e` |
| `--color-line` | `#e5e7eb` | `#2a3242` |
| `--color-ink` | `#171717` | `#e6e9ee` |
| `--color-ink-soft` | `#6b7280` | `#98a1b0` |
| `--color-accent` | `#171717` | `#e6e9ee` |
| `--color-ink-hover` (new) | `#262626` | `#262d3b` |

Light values stay in `@theme`. Dark overrides applied under `html[data-theme="dark"]` and, inside `@media (prefers-color-scheme: dark)`, under `html[data-theme="system"]`.

`color-scheme: light` / `dark` is set alongside the tokens so scrollbars and form controls match the palette.

## `.btn-primary` fix

`.btn-primary` currently hardcodes `hover:bg-neutral-800`. Change to `hover:bg-ink-hover` using the new token. Correct in both themes; removes the last hardcoded color in global.css. `::selection` needs no change — it uses tokens and swaps automatically.

## Theme resolution & no-flash (Layout.astro)

Inline script in `<head>`, before any paint:

1. Read `localStorage.theme` (`light` | `dark` | `system`).
2. Invalid or missing → `system`.
3. Set `document.documentElement.dataset.theme` and `color-scheme` accordingly.
4. Storage access failure (private browsing) → catch, fall back to `system`.

## Toggle (Header.astro)

- Icon button in the header, right of the nav links: sun / moon / monitor inline SVGs, no dependency.
- Click cycles light → dark → system; writes `localStorage`, updates `data-theme`, icon, and `aria-label`.
- Listens for `matchMedia('(prefers-color-scheme: dark)')` changes so `system` follows live OS switches.
- Button renders with a sensible server-side default; the init script syncs icon/label on load to avoid mismatch.

## Files touched

- `src/styles/global.css` — token overrides, `ink-hover` token, `.btn-primary` fix, `color-scheme`
- `src/layouts/Layout.astro` — inline init script
- `src/components/Header.astro` — toggle button + cycle logic

## Verification

- `astro build` passes.
- In dev server: toggle cycles all three states; choice persists across reload; OS preference change applies while in system mode; no flash of wrong theme on hard reload; cards, buttons, header, and selection render correctly in both palettes.
