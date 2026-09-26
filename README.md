# What a cleared hectare is worth

A four-page static site presenting a municipal panel of the Brazilian Legal
Amazon: does deforestation-driven growth deliver the development it is traded
for?

| Page | Holds |
|---|---|
| `index.html` | The argument — Harvey, the question, the hypotheses, the results in plain language, and what failed |
| `maps.html` | All nine figures, each with what it shows **and** what its construction is deciding |
| `methods.html` | Every source, every join with its measured error rate, every decision that could have gone otherwise |
| `formulas.html` | Every equation, hand-set in HTML — no math library, no dependency |

No build step, no framework, no JavaScript. Three HTML files, one stylesheet and
nine PNGs.

## Publishing it on GitHub Pages

The simplest route — the repository root *is* the site:

```bash
cd site
git init
git add .
git commit -m "Amazon decoupling site"
git branch -M main
git remote add origin git@github.com:<you>/<repo>.git
git push -u origin main
```

Then in the repository: **Settings → Pages → Build and deployment → Source:
Deploy from a branch → `main` / `/ (root)`**. It appears at
`https://<you>.github.io/<repo>/` within a minute or two.

If you would rather keep the site inside the existing analysis repository, copy
this folder in and point Pages at it instead — but note that the analysis repo
already has a `docs/` directory of working notes, so serve from a branch rather
than from `/docs` or the two will collide.

`.nojekyll` is included so GitHub serves the files as they are instead of
running them through Jekyll.

## House style

White ground (`#FFFFFF`), Archivo for text and display, IBM Plex Mono for data
and labels, Viridis for every data colour. The figures are rendered on the same
white, so a figure sits on the page with no visible plate edge. Single theme by
choice: the PNGs have a baked-in white ground and a dark mode would fight every
one of them.

Regenerating the figures after any change to the analysis:

```bash
python src/05_figures/fig_core.py && python src/05_figures/maps.py
cp figures/*.png site/assets/figures/
```

## Checking a number

Everything quoted on the site is written to a file by the pipeline before it is
quoted. The headline growth estimates are in `results/rung3_panel_fe.csv`, the
welfare long differences in `results/welfare_hansen.json`, the conflict edges in
`results/conflict_edges.json`, and the case-concentration measure in
`results/case_concentration.csv`.

## Attribution

Sahasrik Ragani. Data from INPE (PRODES, DETER), IBGE (SIDRA, the agricultural
censuses, the municipal mesh), the Atlas do Desenvolvimento Humano no Brasil,
the University of Maryland Global Forest Change product, and the Comissão
Pastoral da Terra. All currency in constant 2023 reais.
