# House Price Prediction with a Neural Network

A Keras neural network that predicts house sale prices on the King County (Seattle area) dataset: 21,613 sales and 21 columns, including bedrooms, bathrooms, living area, grade, condition, waterfront, view, year built, latitude and longitude.

Everything lives in one notebook: `House-Price-Prediction.ipynb`.

## What the notebook does

1. **Explore:** load the data, check for missing values, look at price by year and month.
2. **Prepare:**
   - drop `id` and `zipcode`
   - turn `date` into `month` and `year`
   - predict `log(1 + price)` instead of the raw price, because prices are heavily skewed
   - scale features to 0–1 (`MinMaxScaler`)
   - split 70% train and 30% test
3. **Model:** two hidden layers (128 and 64 units, ReLU), L2 regularization and 30% dropout, Adam optimizer, mean squared error loss, 100 epochs.
4. **Evaluate:** error on the held-out test set, plus a predicted-vs-true price plot.

## Results (test set, log-price scale)

| Metric | Value |
|---|---|
| MAE | 0.153 |
| RMSE | 0.211 |
| Explained variance | 0.844 |

These are on the log scale, so an MAE of 0.153 means predictions are typically around 16% away from the real price. The final cell converts predictions back to dollars and prints the MAE in dollars; re-run the notebook to see it.

## Run it

```bash
git clone https://github.com/SAKETTTTT/House-Price-Prediction.git
cd House-Price-Prediction
pip install -r requirements.txt
```

1. Download `kc_house_data.csv` ("House Sales in King County, USA" on Kaggle) and put it in this folder. The data file is not included in the repo.
2. Open `House-Price-Prediction.ipynb` in Jupyter and run the cells from top to bottom.

## Ideas for next steps

- Compare against simpler baselines (linear regression, random forest, XGBoost) to see how much the neural network actually helps.
- Try cross-validation and hyperparameter search instead of a single train/test split.
- Use `zipcode` and location features (it was dropped here).
- Check which features matter most.
