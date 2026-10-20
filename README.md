# Rock strength from surface drilling data

**An exact null direction in the drag-bit model and what it means for sanding-risk decisions**

This repository holds the cleaned data and the complete analysis code for the paper of the same title. The paper is under review, and its full reference will be added here once it is published.

## Files

| File | Contents |
|---|---|
| `Topic4_MSE_Strength_CODE.ipynb` | Executed notebook with every line of code: cleaning, the forward model, the synthetic profiles, the three inversion routes, MCMC, the robustness runs, the field inversion on the two PDC runs, the figures and every number quoted in the paper. The notebook writes its own helper scripts as it runs. |
| `Topic4_MSE_Strength_CLEANED_DATA.csv` | The cleaned drilling record, one row per raw record sorted by depth, with the bit record, lithology, operating flags and MSE at the actual bit size. |
| `Topic4_MSE_Strength_SCENARIOS.csv` | The 80 synthetic strength profiles, with their true parameters and the results of every route. |
| `Topic4_MSE_Strength_SCENARIO_LAYERS.csv` | One row per profile and 25-ft layer: the true strength, the Route 1 and Route 2 layer estimates, and the Route 2 contrast uncertainties with and without a calibrated layer. |
| `Topic4_MSE_Strength_CLEANED_DATA_dictionary.txt` | Column definitions and units for all three CSV files. |
| `field_data.csv` | The raw drilling record the notebook starts from, a copy of the public Pason log of the well. |
| `stored_results/` | The stored batch results of the runs used for the paper (the inversions on all 80 profiles, the network runs, MCMC, the robustness cases and the field inversions), which the notebook reads in its default mode. |
| `requirements.txt` | The Python packages the notebook needs. |

## Running the code

Python 3.12 or later.

```
pip install -r requirements.txt
jupyter notebook Topic4_MSE_Strength_CODE.ipynb
```

Keep all the files in one folder; the notebook reads `field_data.csv` from the folder it is run in and works inside `topic4_work/`. It has two run modes, set by `FULL` in the first code cell.

- `FULL = True` re-runs every batch from scratch: both inversion routes with profile likelihoods on the 80 profiles, the networks, MCMC, the robustness inversions and the field inversions. This takes several hours on two cores.
- `FULL = False` (the default) rebuilds the cleaned record and all synthetic profiles, re-runs the inversions on two profiles and the whole field application (about a minute), and draws the remaining figures from the stored batch results in `stored_results/`.

The executed notebook in this repository already shows the output of every cell from the runs used for the paper.

## Data sources

All data come from Utah FORGE well 58-32 (MU-ESW1), a geothermal test well near Milford, Utah, released through the Geothermal Data Repository under a CC BY 4.0 licence.

- Drilling record: Podgorney, R., McLennan, J., Moore, J., 2018. *Utah FORGE: Drilling Data for Student Competition*. Geothermal Data Repository. https://doi.org/10.15121/1495411
- Bit record, daily drilling reports and end-of-well report: Nash, G., Moore, J., 2018. *Utah FORGE: Logs and Data from Deep Well 58-32 (MU-ESW1)*. Geothermal Data Repository. https://doi.org/10.15121/1452735
- Core tests: McLennan, J., 2018. *Utah FORGE: Well 58-32 Core Analyses*. Geothermal Data Repository. https://doi.org/10.15121/1557418

The cleaned files here are derived from these records. If you reuse them, please cite the original data sets, as their licence requires, and the paper.
