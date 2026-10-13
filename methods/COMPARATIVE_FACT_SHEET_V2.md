# Comparative fact sheet v2

Report-only aggregation and presentation layer. No GRASS task or scientific receipt is recalculated or replaced.

Adds:

- stock comparison for Brazil and each biome;
- size-class comparison for Brazil and each biome, by year;
- absolute, V2−old, and percent-difference views;
- exact event count + event mean-area time series by biome/year;
- split area views: source mean, child mean, total children area per split;
- merge area views: target mean, source mean, total source area per merge;
- compact latest-year biome event comparison table;
- downloadable `classes_area_anuais_pais_bioma.csv`;
- downloadable `eventos_areas_bioma_ano.csv`.

Event-area biome series use the audited `level=biome` record from the second-pass event-area results. They are **not** computed as a simple mean of municipality means.

Percent differences are left unavailable when the old collection is zero.
