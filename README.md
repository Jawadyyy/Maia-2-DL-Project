# Reproducing Maia-2 (NeurIPS 2024): human move prediction in chess

CS-444 Deep Learning, Assignment 2, Air University.
Team: Jawad Mansoor, Muhammad Ali Khan, Waqas Siddique.

We reproduce **Table 1** of *Maia-2: A Unified Model for Human-AI Alignment in Chess* (Tang et al., NeurIPS 2024):
top-1 accuracy at predicting the move a human plays, for each skill group (Skilled < 1600, Advanced 1600–1999, Master ≥ 2000).
We also **train Maia-2 from scratch** with the official training code on the officially released example games, and add a skill-blind analysis.

| | |
|---|---|
| Paper | https://openreview.net/forum?id=XWlkhRn14K · https://arxiv.org/abs/2409.20553 (DOI 10.48550/arXiv.2409.20553) |
| Official code | https://github.com/CSSLab/maia2 (MIT), commit `67bee6ce7e2f264344fe6d2026a2e18c76a82efa` |
| Data | Lichess rated Rapid games (https://database.lichess.org/), via the official `maia2.dataset` loaders (Maia Testset: 106,740 positions; example training PGN: 28,196 games) |
| Model | ResNet CNN board encoder + skill-aware attention + policy / auxiliary / value heads (23.3M parameters) |
| Main metric | Top-1 move accuracy, averaged over the 3 skill groups (paper: **53.25%**) |

## How to run (Google Colab)

1. Open `maia2_reproduction.ipynb` in Colab and choose **Runtime → Change runtime type → T4 GPU**.
2. Leave `SMOKE_TEST = True` and select **Runtime → Run all** (about 10 minutes). This checks the whole pipeline.
3. Set `SMOKE_TEST = False` and select **Run all** again for the real experiment.
4. Outputs (results tables, figures, logs, environment record, predictions, and a zip of everything) are saved to `MyDrive/maia2-reproduction/full/`.

No accounts or tokens are needed.

## Deviations from the paper

| | Paper | Ours | Why |
|---|---|---|---|
| Table 1 evaluation | released Maia-2 Rapid model, Maia Testset | the same checkpoint and test set (group sizes match exactly) | none |
| Training data | 169M games / 9.1B positions | 28,196 example games | compute: the paper trained for 13 days on 2× A100 |
| Batch size | 8192 | 2048 | T4 memory (16 GB) |
| Balancing cap | 20 games per rating pair per chunk | off (all games kept) | the cap is designed for monthly files with millions of games |
| Software | torch 2.8 (package pin) | Colab's preinstalled torch (recorded in `environment.json`) | Colab compatibility |

Results: see `results/` once the notebook has run (files are written to Drive and copied here).
