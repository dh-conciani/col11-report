# Selectable standardized lineage · Top 10 Brasil + biomas

This analysis is **not** the native V2 genealogy. It reconstructs a comparable overlap-lineage for `col11_old_track` and `col11_v2_track` from the already verified spatial `edges.parquet` ledgers, using the same identity rule on both products.

## Ranking used by the selector

For every root, the task computes annual active-track count and ranks roots by:

`track_change_total = Σ | active_tracks(year) - active_tracks(year-1) |`

The first appearance is measured against zero. If a lineage ends before 2025, the final transition back to zero is also included. `area_change_total_ha` and lineage size are deterministic tie-breakers only. This gives an interpretable ranking of **largest cumulative temporal changes**, without mixing counts, hectares and event types into an arbitrary composite score.

Each biome/product task caches the Top 10 roots. The Brazil Top 10 is obtained by pooling the 60 biome candidates for each collection and applying the same ranking. A root outside the Top 10 of its own biome cannot enter the national Top 10 because at least ten roots in that same biome already have a higher score.

Old and V2 roots are selected independently. Comparing rank 1 vs rank 1, or any other pair chosen in the report, is a rank-to-rank comparison and **does not imply spatial homology** between the roots.

## Cached series

Each verified task writes:

- `summary.json`
- `annual.csv` — default Top 1 series
- `root_ranking.csv` — audited ranking table
- `top10_annual.csv` — 10 roots × 40 years
- `top10_track_history.csv` — exact fragment ID history of each Top-10 root track
- `standardized_lineage.done.json`

The method version is `standardized_overlap_lineage_v2_selectable_top10`. Results created by v1 are treated as stale and safely archived on rerun. No GRASS task or spatial transition ledger is recomputed.

## Map cache

After all 12 tasks are verified and `comparison.json` exists, run:

```bash
bash compare/STANDARDIZED_LINEAGE_MAP_CACHE.sh --build --jobs 2
```

The map cache creates one image per Top-10 root in every biome/product task: **120 images total**. The national selector reuses those same cached images and does not duplicate files.

Each image maps the **root track itself** at up to three observed snapshots (first, middle, last), with one fixed extent across panels and exact masking to the corresponding biome. The report metrics still describe the complete lineage, including descendants. This distinction is printed in the map caption.

The cache is stored under:

`compare/results/standardized_biome_lineage/map_cache/`

and has a checksum-verified `manifest.json` and `map_cache.done.json`. Final release QA requires all 120 maps.

## Recommended sequence

```bash
bash compare/STANDARDIZED_BIOME_LINEAGE.sh --plan
bash compare/STANDARDIZED_BIOME_LINEAGE.sh --run --biome all --product all --jobs 2 --confirm-large-run
bash compare/STANDARDIZED_BIOME_LINEAGE.sh --status

bash compare/STANDARDIZED_LINEAGE_MAP_CACHE.sh --plan
bash compare/STANDARDIZED_LINEAGE_MAP_CACHE.sh --build --jobs 2
bash compare/STANDARDIZED_LINEAGE_MAP_CACHE.sh --status

bash compare/UNIFIED_REPORT.sh --auto-maps --promote-main
bash compare/RELEASE_REPORT.sh
```

The report defaults to **Brasil · rank 1** for both collections, but all Top-10 roots for Brasil and each of the six biomes are already in the HTML data/cache and can be selected interactively.
