# pashtoun.com

The source for [pashtoun.com](https://pashtoun.com), my personal site.

I build new lines of business in professional services, from idea to flywheel. Away from work, I'm a game master, a Wing Chun instructor, a cook who loves hosting dinner parties, and someone who keeps time by the moon and the seasons. The site tries to say all of that in one quiet page.

## A page that follows the sky

The site works like a small almanac. Every time it loads, it works out where we are in the lunar month and the year, and the page changes to match.

- **Tonight's moon.** The moon at the top is drawn live in the browser for the current date, along with its phase name, how much of it is lit, and the number of days until the next full or new moon.
- **The season.** The accent color follows the season: slate blue in winter, moss in spring, honey in summer, and oxblood in autumn. A line under the moon counts down to the next solstice or equinox.

### How the moon is calculated

The phase comes from the moon's age: the number of days since a known new moon (January 6, 2000, 18:14 UTC), taken modulo the length of a synodic month (29.530588853 days).

- **Illumination** is `(1 − cos(2π × age ÷ 29.53)) ÷ 2`.
- **Phase names** follow eight equal divisions of the cycle, from new moon through waxing crescent, first quarter, waxing gibbous, full, waning gibbous, and last quarter to waning crescent.
- **The drawing** is a single SVG path. One semicircle traces the lit edge, and half of an ellipse traces the terminator, the line between day and night on the moon. The ellipse's width is `|cos(2π × phase)| × r`, which bulges toward the dark side for a crescent and toward the lit side for a gibbous moon.

The result is accurate to within about a day, which is plenty for an almanac you read by eye. The moon is drawn as it appears from the Northern Hemisphere, lit on the right while waxing.

### How the seasons are calculated

The page uses approximate Northern Hemisphere turning dates: March 20, June 21, September 22, and December 21. It sets a `data-season` attribute on the page, and CSS variables swap the accent color from there.

## Set in the spirit of LaTeX

I've typeset my resumes in LaTeX for years, a habit from writing math in college. The site borrows that look: a Computer Modern–style serif (Latin Modern when it's installed), small-caps section headings, the LaTeX logo in the footer, and an end-of-proof mark (∎) to close the page.

## Built to be simple

- **One file.** Everything lives in `index.html`: HTML, CSS, and one short script.
- **No dependencies.** There's no framework, build step, web font service, or analytics, and nothing tracks you.
- **Light and dark.** The page follows your system's color scheme, with its own palette for each.
- **Accessible.** It uses semantic headings, a labeled moon image whose description updates with the phase, visible keyboard focus, and layouts that work down to phone width.

## Running it locally

Open `index.html` in any browser. That's it.

## Deployment

The site is hosted on [Netlify](https://www.netlify.com), which publishes the `main` branch on every push. There's no build command, and the publish directory is the repository root.