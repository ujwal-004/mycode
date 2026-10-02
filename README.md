# LeakGuard: code for the credit-card fraud evaluation experiments

Code accompanying the paper *LeakGuard: A Leakage-Controlled Evaluation Methodology for Credit-Card Fraud Detection*.

## Data

Download `creditcard.csv` from the Kaggle ULB dataset
(https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud) and place it in the same
folder as the notebooks (in Colab, upload it to the session). The notebooks check for
284,807 rows and 492 frauds, then drop missing values and exact duplicates, leaving
283,726 transactions (473 frauds).

## Notebooks

| Notebook | What it produces |
|---|---|
| `enhanced_fraud_detection_ipynb_txt.ipynb` | Predefined baselines (Table II), confusion matrix of the tuned Random Forest (Fig. 2), sampler comparison (Table IV, Fig. 3a), ten-seed baseline analysis (Table VI) |
| `second_version.ipynb` | Random Forest grid-search CV AP values, tuned models for Decision Tree, LinearSVC, MLP and XGBoost (Table III), training-OOF threshold selection (Table V, Fig. 3b), environment record |

Run each notebook from top to bottom. The full main notebook takes about 3 hours on the
free Colab tier; the Random Forest grid search in `second_version.ipynb` takes about 35 minutes.

## Setup

Recorded environment: Linux, 2 CPU threads, about 12 GiB RAM, Python packages as pinned in
`requirements.txt`. Install with `pip install -r requirements.txt`. Random state 42 is used
where supported; the ten-seed analysis uses seeds 42, 7, 13, 21, 99, 55, 77, 3, 17 and 101.

## Notes

- All preprocessing (scaling and resampling) runs inside an `imblearn` pipeline, so it is
  refitted within each training fold during cross-validation.
- Classification thresholds in the paper are chosen from training-only out-of-fold scores
  (`second_version.ipynb`), never from development-holdout labels.
- The development holdout is reused for several comparisons and is not an untouched test set.
- The notebooks contain recorded cell outputs; the numbers in the paper match them.
