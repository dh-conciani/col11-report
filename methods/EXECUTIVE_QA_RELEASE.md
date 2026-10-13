# Executive summary, QA and release

This report-only extension adds six biome executive cards, an audited CSV summary, reproducibility QA, self-contained HTML generation and an immutable release ZIP.

It does not modify GRASS outputs, spatial receipts, territorial receipts, event-area receipts, or source rasters. The highlighted territory in each biome is the city-year/event class with the largest absolute paired count difference among Nascimento, Morte espacial, Divisão simples and Fusão simples.

`compare/RELEASE_REPORT.sh` rebuilds the unified report with the latest verified 48 map exhibits, validates the scientific/report joins, embeds the maps into a portable HTML, writes SHA-256 checksums and packages a timestamped release under `compare/results/releases/`.
