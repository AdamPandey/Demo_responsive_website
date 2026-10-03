# Demo Responsive Website

A one page responsive demo site built with Bootstrap 5.3.3, using a "Transformers Wiki" theme (the hero text is about Orion Pax becoming Optimus Prime). It uses Bootstrap's grid and customises Bootstrap through Sass instead of just linking the stock CSS.

It's a single static page with placeholder links and placeholder card text. Nothing is wired up behind it.

## Tech

- HTML (`index.html`)
- Bootstrap 5.3.3, installed through npm (`node_modules/bootstrap`) and compiled from its Sass source
- Sass, with overrides in `sass/main.scss`
- Bootstrap's JS bundle, loaded from the jsDelivr CDN at the bottom of `index.html` (needed for the navbar toggle, so the collapsed menu needs an internet connection to work)

## Running it

No server or build is needed to view it. Open `index.html` in a browser. It links the already compiled `css/main.css`.

## Changing the styles

The page uses `css/main.css`, which is generated from `sass/main.scss`. `package.json` only lists the dependencies (`bootstrap` and `chalk`) and has no scripts, and Sass itself isn't in the dependencies. So the compile command isn't recorded in this repo, and none has been verified here. With a Sass compiler installed (for example the `sass` npm package), compile `sass/main.scss` to `css/main.css`. The source map `css/main.css.map` next to it shows that's how the CSS was produced. `chalk` isn't used anywhere in the site.

## What's in the Sass

`sass/main.scss` imports Bootstrap's functions, then sets variables, then imports the rest:

- `$primary` is changed from Bootstrap blue to red (`rgb(252, 0, 0)`). That's why the navbar and hero are red.
- Three extra theme colours are added through `$theme-colors`: `tertiary` (orange), `tertiary-light` and `tertiary-dark` (a strong blue). Bootstrap then generates the matching utilities and buttons from them, such as `.btn-tertiary`, and the hero heading uses `text-tertiary-dark`.
- There is an `@each` loop meant to make `.bg-*` light and dark variants, but it doesn't produce any output (it loops over a plain string called `colors`, and `.bg-#{color}` is missing the `$`). It's still in the file, and the compiled CSS has no such classes.
- Everything else is Bootstrap's own `bootstrap.scss` imported at the end.

## Layout and responsiveness

All responsive behaviour comes from Bootstrap's grid and utilities, not from custom media queries.

- Navbar: `navbar-expand-lg` with a fixed top bar. Below the `lg` breakpoint (992px) the links and the search form collapse behind the hamburger button.
- Hero: a `container-fluid` with a two column row (`col-md-6` each). Text on one side, `images/1.png` on the other, stacking on screens narrower than `md` (768px). The image uses `img-fluid`.
- Cards: three Bootstrap cards in `col-md` columns, so they sit in a row from `md` upwards and stack on phones (the "Made cards responsive" commit).
- A row of star icon buttons (inline SVG from Bootstrap Icons) in `col-auto` columns, a box icon, and a final text and image section using `images/2.png`.

## Files

```
index.html       the page
sass/main.scss   Bootstrap overrides and the entry point for compiling
sass/main.css    empty file
css/main.css     compiled output used by the page
css/main.css.map source map
images/          hero, card and section images
package.json     bootstrap and chalk dependencies, no scripts
node_modules/    committed to the repo (see below)
```

## Known gaps

- `node_modules/` is committed (512 tracked files, about 13 MB) and there is no `.gitignore`. It could be removed from the repo and restored with `npm install`, since `package-lock.json` is committed.
- `index.html` has a typo, `<di class="d-flex container-xl">` around the cards, which should be `div`. The browser copes, but the closing tags don't match up.
- The `<title>` is still "Bootstrap demo", and the card text, card titles, buttons, nav links and several `alt` attributes ("...") are Bootstrap placeholders.
- `images/3.png`, `images/1old.png` and `images/headshot.jpg` aren't used by the page.
- `sass/main.css` is an empty file.
- The star buttons and the repeated SVG markup are copy pasted four times.

## History

Eight commits. The first three, on 18 October 2024, are the initial page and making the cards responsive. On 25 October 2024 Bootstrap was added through npm, `sass/main.scss` was set up with the variables and custom colours, and the CSS was compiled. Commits are by Adarsh Pandey.
