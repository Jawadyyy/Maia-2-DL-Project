# Results

`smoke_test/` holds the outputs of the pipeline check (`SMOKE_TEST = True`: 1,998 test positions, 300 training games,
1 epoch, Colab T4, 25 Oct 2026). **They are not the reported results**; they only show that every step runs.
Its executed notebook is `notebooks/maia2_reproduction_smoke_run.ipynb`.

The real results go in the files below. This folder is filled from the Colab run (`SMOKE_TEST = False`). The notebook writes everything to
Google Drive under `MyDrive/maia2-reproduction/full/`, and also saves a zip of it as
`MyDrive/maia2-reproduction/maia2-results-full.zip`. Copy these files here:

| File | Contents | Assignment part |
|---|---|---|
| `environment.json`, `pip-freeze.txt` | software and GPU used | e |
| `data_summary.json` | test and train counts, skill-group sizes, leakage check | d |
| `training_overrides.json` | settings changed from the official config | e |
| `train.log` | timestamped log of the official trainer | e (evidence) |
| `table1_reproduction.csv` | paper vs reproduced Table 1 | f |
| `own_training_by_epoch.csv` | own-trained model accuracy per epoch | f |
| `final_comparison.csv`, `summary.json` | all models with Δ vs the paper | f, g |
| `training_curve.csv` | loss values behind the loss plot | e |
| `figures/*.png` | all plots | g |

Leave out the `predictions_*.csv` files if they are too large for GitHub (each is about 10 MB). They stay in the zip on Drive.

Every number in the report must come from these files. Nothing is entered by hand.
