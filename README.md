# Game-Theoretic-Security-Orchestration-for-Cross-RIC-Policy-Conflicts-in-O-RAN


**Color scheme (consistent across figures):**
- Initial → `lightgray`
- Nash → `green`
- Cooperative → `yellow`
- Stackelberg → `pink`

---

## Requirements

- Python 3.8+
- NumPy
- Pandas
- Matplotlib
- (Optional, for inline preview) IPython

> In Google Colab these libraries are preinstalled. The code saves figures under `/content/Project8`.

---

## How to run

1. Open a Jupyter/Colab notebook.
2. Copy the code cells **in order** (Cells 1 → 9).  
3. Run all cells.  
4. See the saved PNGs in `/content/Project8` and the inline preview at the end (Cell 9).

---

## Project anatomy (by cells)

- **Cell 1 – Setup & Reproducibility**  
  Imports, output directory (`/content/Project8`), fixed random seed.

- **Cell 2 – Data Models & Helpers**  
  `SecurityStrategy`, `AppPlayer`, and normalization helpers:  
  - `norm_enc(x) = (x-1)/4`  
  - `norm_ord(x) = (x-1)/4`  
  - `norm_rot(h) = (48-h)/44` mapping `h ∈ [4,48]` to `[1,0]`.

- **Cell 3 – Conflict Detector & Utility**  
  Thresholded divergence penalties and utility composition.

- **Cell 4 – Solvers**  
  Best-response (Nash), log-NSW coordinate ascent (Coop), and simple Stackelberg scan.

- **Cell 5 – Scenario Generator**  
  Creates player populations & strategy menus per scenario; sets rotation thresholds.

- **Cell 6 – Evaluation Loop**  
  Runs all models, times them, builds tidy DataFrames (`avgsec_df`, `latency_df`).

- **Cell 7 – Figure 1**  
  Average Security bars (colored by model) for three scenarios.

- **Cell 8 – Figure 2**  
  Latency bars (colored by model) for three scenarios.

- **Cell 9 – Quick Preview**  
  Displays the saved figures inline (optional).

---

## Customization tips

- **Number of players / strategies:**  
  In **Cell 6** (evaluation) or **Cell 5** (generators) adjust `N` and `m`.

- **Scenario mix & thresholds:**  
  In **Cell 5**, tweak `sec_cnt`, `perf_cnt`, and `tau_rot`.

- **Utility weights:**  
  In **Cell 3 → `UtilityCalculator`**, edit `W_SEC`, `W_OHD`, or player weights `(alpha, beta, gamma)` in **Cell 5**.

- **Output directory:**  
  In **Cell 1**, change `OUTDIR = Path("/content/Project8")` to your preferred path.

- **Colors:**  
  In **Cells 7 & 8**, edit the `color_map` dictionary.

---

## Reproducibility

- `np.random.seed(7)` is set in **Cell 1**.  
- Strategy menus are deterministic (via `linspace`).  
- Player weights are sampled from fixed ranges but under a fixed seed.

---

## Troubleshooting

- **Matplotlib “FixedFormatter” warning:**  
  If you see: _“FixedFormatter should only be used together with FixedLocator”_, it’s safe to ignore for categorical bars.  
  Optional fix (not required): set explicit tick positions:
  ```python
  ax.set_xticks(range(len(models)))
  ax.set_xticklabels(models, rotation=20, ha="right")
  
