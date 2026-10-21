# Predicting Steam Game Popularity with Machine Learning

Can a game's public metadata predict how popular it will be? This exploratory machine-learning project uses **peak concurrent players (CCU)** as a proxy for popularity, because game sales are not publicly available. It evaluates how far genre, platform support, and tag count can explain popularity across a May 2024 snapshot of 87,806 Steam games.

This is a research prototype, created at the University of Applied Sciences Salzburg. Its central finding is as useful as its models: public metadata alone does not reliably predict commercial success. Important drivers such as marketing spend, studio reputation, and launch timing are absent from the data.

## Highlights

- Explores and prepares a real-world Steam catalogue.
- Establishes a mean-prediction baseline, then evaluates XGBoost with three-fold cross-validation.
- Encodes genres safely and derives an interpretable tag-count feature.
- Includes a holdout-set prediction plot for an honest final model check.
- Provides an optional GAN augmentation experiment that runs locally and never writes generated data to the repository.
- Documents limitations, including proxy targets, selection bias, and missing business context.

## Evaluation

The target is `log1p(peak_ccu)`, and lower RMSE is better. The notebook reports the mean and standard deviation of three validation folds for both a mean-prediction baseline and XGBoost. It then evaluates the selected model on a separate holdout set.

XGBoost is used because the data is tabular. This avoids imposing a false sequence order on genre, platform, and tag-count features.

## Run locally

The project is implemented in [Project.ipynb](Project.ipynb). Python 3.10 is recommended.

```bash
python -m venv .venv
.venv\Scripts\activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
jupyter lab
```

Download `games_may2024_full.csv` from Kaggle's [Steam Games Dataset](https://www.kaggle.com/dsv/11017460), then place it here:

```text
BestBet/games_may2024_full.csv
```

The dataset and generated files are deliberately excluded from version control. Review the dataset's Kaggle licence and terms before downloading or using it.

## Project structure

```text
Project.ipynb       Analysis, modelling, and interpretation
requirements.txt    Reproducible Python environment
.gitignore          Excludes data, generated files, and local settings
```

## Limitations

- Peak CCU measures concurrent activity, not sales or long-term profitability.
- Genre, tag count, and platform availability cannot represent major factors such as budget or marketing.
- A generated augmentation file is not included because it was too large and did not provide a reliable, shareable training artifact.
- The optional GAN experiment is disabled by default and must be assessed against the non-augmented holdout result; generated records are not treated as ground truth.
- Results should be read as an investigation of the data and modelling process, rather than a production predictor.

## Data attribution

The analysis uses the May 2024 snapshot from Kaggle's Steam Games Dataset. The raw data is not redistributed in this repository.
