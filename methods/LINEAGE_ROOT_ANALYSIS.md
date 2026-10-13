# COL11 V2 — Root lineage analysis

This report-only extension analyses the finalized V2 lineage registry. It does not rewrite lineage science or spatial-comparison receipts.

## Selection and direct-child semantics

The selected root is the `root_id` with the largest **accumulated** number of distinct track identities whose `primary_parent_track_id` equals that root. For the selected root, these rows must all have `generation = 1`; the analysis now fails closed if any direct-parent row falls outside generation 1. Ties are resolved by larger `n_tracks_ever`, then smaller `root_id`. Total descendants are `n_tracks_ever - 1`.

“Accumulated direct children” covers the full temporal window. It is not the number of children produced by a single split event. A single split topology is reported separately from `lineage_events.csv.gz`.

The preferred source is the canonical finalized run:

`results/track_id/lineage_runs/consolidated_1986_2025/tables/root_registry.csv.gz`

If it is unavailable, discovery is explicit; the tool refuses ambiguous noncanonical sources.

## Native event status

Native lineage split/merge events retain their event-status semantics. Maxima are reported separately for:

- `CONFIRMED` events;
- `RIGHT_CENSORED` events.

The backward-compatible fields `largest_split_children` and `largest_merge_parents` now refer only to the `CONFIRMED` maxima. A right-censored event, especially at the terminal year of the series, is never presented as the confirmed maximum.

## Derived outputs

The analysis reports accumulated direct children, total descendants, generation depth, annual active tracks, annual aggregated lineage area, birth/expansion years, confirmed native split/merge counts, separate confirmed/right-censored topology maxima and years, top direct children, and a ranking of roots by accumulated direct children.

When `root_id_YEAR.tif` and `track_id_YEAR.tif` are available, real raster views are generated for the first observed year, peak simultaneous-track year, and latest observed year. Duplicate years are emitted only once.

Native lineage split/merge events are not substituted for the standardized old-vs-V2 spatial-transition metrics in the comparison report.
