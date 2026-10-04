# Daniel Njoroge: portfolio site

A single-page portfolio for Daniel Kimani Njoroge, a geomatics engineer and drone pilot. No build step: it's one `index.html` plus a few assets.

```
index.html                       the whole site (HTML, CSS and JS)
assets/world-110m.js             Natural Earth 1:110m countries for the coverage map (public domain)
assets/fimbul-gpr-flight.jpg     M350 RTK + GPR over the Fimbul Ice Shelf (featured project)
assets/gpr-rig.jpg               the survey rig (GPR case study)
assets/ugcs-test-plan.jpg        UgCS plan, Contermanskloof test flight
assets/vineyard-rendvi.jpg       red-edge NDVI map, Quinta de Baixo (with legend)
assets/vineyard-rendvi-field.jpg same map cropped for the project card
assets/vineyard-orthomosaics.jpg RGB orthomosaics of the three vineyards
```

## Where the content came from

All the text comes from Daniel's own documents. Nothing on the page is invented.

- In his Claude account: the CV (GIS Analyst), the CV (Drone Pilot), the Drone Survey Portfolio and the Heritage Watch cover letter.
- On his computer:
  - `Daniel_Kimani_Njoroge_CV.pdf`
  - the signed SAGC Work-Integrated Learning schedule (`Daniel Kimani WIL.pdf`), which is the source for the project register and the WIL chart
  - `5dGeo projects ive been involved in.docx`, used only to confirm scope

The photos come from the Drone Survey Portfolio.

Privacy choices:
- **Client names, client contacts and private addresses** from the 5D Geo briefs are deliberately left out. Projects are described by site type and area, the same way the CV does it.
- **Personal details** (date of birth, home address, the Botswana number, referees' contacts) are not published.
- **Map pins**: where an exact site isn't public, the pin sits in the region (marked with `data-approx` on the project card).

## Still to do

- **Photo of yourself (optional)**: in the About card, replace the canvas and the "DN" monogram with `<img src="assets/portrait.jpg" alt="Daniel Njoroge">`.
- **Contact form**: out of the box it opens the visitor's email app. To receive messages directly, create a free [Formspree](https://formspree.io) form and paste its URL into `formEndpoint` in the `SITE` settings at the top of the main `<script>`.
- **Phone number**: it's shown in the Contact section because it's on your CV. Delete that row if you'd rather not publish it.

## Editing

- **Settings**: the `SITE` object at the top of the main `<script>` holds the email, home city (which drives the hero coordinates and map marker), map extent, polar inset and form endpoint.
- **Projects**: each `<article class="project">` holds:
  - `data-cat`: the filters (`uav`, `lidar`, `rs`, `gis`)
  - `data-lat` / `data-lon` / `data-place`: the map pin (leave these out and there's no pin)
  - `data-approx`: shows the place name instead of exact coordinates
  - `data-client`
  - the `<template>`: the case-study text; figures are allowed
  - Use `<img class="tile">` for a photo, or `<canvas class="tile" data-tile="...">` for a generated map tile (`parcels`, `trees`, `scan`, `routes`, `pipes`, `island`, `stockpiles`, `change`, `ndvi`, `hyps`).
- **Project register**: one `<li class="reg-row">` per job, newest first. Add `<button class="reg-case" data-case="p-...">` to link a row to a project card's case study (by the card's `id`). The count and the "Show all" button update automatically.
- **WIL chart**: each `<tr class="wil-row">` sets its bar width (days ÷ 50) and minimum tick (minimum ÷ 50) as inline percentages, so it reads correctly without JavaScript. Update `data-days` and `data-min` too, since the hover tooltip reads them.
- **Countries**: edit `<ul id="country-list">`. Names must match Natural Earth (add `data-ne` if the display name differs).
- **Experience**: `data-start` / `data-end` as `YYYY-MM`, or `data-spans="2024-01:2024-02,2024-06:2024-07"` for split stints. Durations and the timeline chart are calculated automatically.

## Run locally

```bash
python -m http.server 8765
```

Then open http://localhost:8765.

## Deploy (free)

- **GitHub Pages** (you already have the `danzo111` account): create a repo, push this folder, then go to Settings → Pages → Deploy from branch → `main` / root. The site appears at `https://danzo111.github.io/<repo>/`, or at `https://danzo111.github.io/` if the repo is named `danzo111.github.io`.
- **Netlify**: drag the folder onto https://app.netlify.com/drop
- **Custom domain** (for example `danielnjoroge.com`): add it in your host's settings and point your DNS where it tells you.

## Credits

Map data from Natural Earth via `world-atlas`. Fonts are Archivo, Newsreader and Martian Mono (Google Fonts). The page loads D3 and TopoJSON from cdnjs.
