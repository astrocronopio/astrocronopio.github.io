# evecoronel.com

Personal and professional website of Evelyn Coronel. Static HTML, one shared
stylesheet, no build step.

## Structure

- `index.html` redirects to `about.html`.
- `home.html` is the personal side. `about.html` is the professional side.
- `media/writings/` holds personal texts. `media/blog/` holds tech posts.
  `media/blog/one-month-of-learning.html` is the day-by-day log of the 2026
  learning month; entries are hand-maintained and dated by first commits.
- `style.css` styles every page. `version.js` prints version and date.
- `theme.js` runs the light and dark theme toggle.

## Theme system

All colors live in CSS custom properties on `:root` in `style.css`.

- Dark is the default theme. It matches the artwork backgrounds.
- Each side has an accent: lavender for personal, amber for professional.
  `body.about` switches the accent. Pages without a body class get lavender.
- Light mode inverts the surface tokens and darkens the accents for
  contrast. The background artwork stays in both themes. A `body::before`
  scrim darkens the edges in dark mode and adds a daylight haze in light
  mode.
- The toggle button sets `data-theme="light"` on `<html>` and stores the
  choice in `localStorage` under the key `theme`. `theme.js` loads in
  `<head>` so the stored theme applies before first paint.
- The toggle button ships with the `hidden` attribute. `theme.js` reveals
  it, so the button never shows without JavaScript.

## Backgrounds

Each page sets its own wallpaper: `body.home` and `body.about` in
`style.css`, and inline `<style>` blocks in the writing pages. New pages
can do either.
