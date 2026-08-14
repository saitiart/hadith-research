# Information Flux in Hadith Transmission

Code and data for the paper. Models isnad transmission as a conserved flow
on a DAG: material is injected at root narrators, routed teacher → student
in proportion to recorded transmissions, and absorbed at the collector.

    (I - P) ρ = S

Because transmission is strictly teacher-to-student, `P` is nilpotent under
a generation ordering and the system solves exactly in one forward pass.

## Requirements

    numpy pandas networkx scipy matplotlib

## Data

- `all_narrators_global.json` — narrator metadata
- `sahih_al_bukhari_clean.json`,
- `sahih_muslim_clean_full.json`
- `/nasai_clean_full.json`
- `/sahih-muslim/sahih_muslim_clean_full.json`
  — traditions with their chains, Bukhari and Muslim are are more robust, Tirmidhi and AbuDawud are less, which is why they were not used in the first place

## Running


The __main__ prints network diagnostics, preprocessing drop shares, conservation, the
ablation table, per-generation concentration, and the plots

## What the numbers are

| quantity | meaning |
|---|---|
| `rho` | flux — material routed through each narrator |
| `nu` | depth — nodes remaining to the collector |
| `solo` | σ({u}), delivered flow lost if u is removed |
| `cumulative` | σ(K), u removed together with all ranked above him |
| `stranded` | material entering orphans, never delivered |

## Parameters

- `GEN_CAP = 4` — vertical edges spanning more generations are discarded
- Lateral (same-ṭabaqa) edges are excluded: a ṭabaqa gives no ordering
  evidence within itself. Their mass share is reported as `lateral_share`.

## Reproducing the paper

Tables 2–3 come from `ablation(M)`; Table 1 from `M['diag']`; the Gini
figures from `concentration(M)`; the centrality correlations from
`centrality_baseline(M, ablation(M))`. Run once per collection.

## Notes

Plotting code was written with generative AI assistance; All figures reported in the paper were
verified against this code.

MIT licence.