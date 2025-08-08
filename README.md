# Analysis of Trader Behavior vs. Market Sentiment

This repository contains the full analysis for the Data Science assignment from the Web3 Trading Team. The project explores the complex relationship between the behavior of individual traders and the prevailing market sentiment (Fear vs. Greed) to uncover actionable, data-driven insights for smarter trading strategies.

The analysis progresses from a high-level market overview to an advanced, multi-layered approach involving unsupervised clustering to discover trader "personas" and state-of-the-art SHAP explainability to identify the key drivers of trade profitability.

## Directory Structure

The repository is organized according to the specified submission format:

```
ds_shreyas_n/
│
├── notebook_1.ipynb                # Main Google Colab notebook with all analysis
├── ds_report.pdf                   # Final summarized report with insights and explanations
├── README.md                       # Project overview and instructions (this file)
│
├── csv_files/                      # Directory for all data files
│   ├── fear_greed_index.csv
│   └── historical_data.csv
│
└── outputs/                        # Directory for all visual outputs
    ├── time_series_volume_vs_sentiment.png
    ├── trader_profile_features_clustermap.png
    ├── kmeans_elbow_method.png
    ├── trader_persona_radar_chart.png
    ├── pnl_distribution_ridgeline_plot.png
    ├── shap_global_feature_importance.png
    └── shap_summary_dot_plot.png
```

## Methodology

The analysis was conducted in a sequential, multi-stage process to build insights from the ground up.

#### 1\. Data Preprocessing & Merging

  * The raw historical trader data and the daily Fear & Greed Index data were loaded.
  * Timestamps were standardized, and the two datasets were merged on the 'date' field to create a unified dataset where each transaction is mapped to the market sentiment of that day.

#### 2\. Exploratory Data Analysis (EDA)

  * A market-level analysis was performed to understand broad patterns. This involved comparing trading volume, profitability (PnL), and buy/sell ratios against the two main sentiment categories: 'Fear' and 'Greed'.

#### 3\. Unsupervised Clustering for Persona Discovery

  * To gain deeper insights, the analysis shifted from a market-level to a trader-level view.
  * A profile of behavioral features was engineered for each unique trader account (e.g., average trade size, win rate, sentiment preference).
  * **K-Means clustering** was applied to these profiles to segment traders into distinct, data-driven "personas." The optimal number of clusters was determined using the Elbow Method.

#### 4\. Predictive Modeling & SHAP Explainability

  * A predictive model (**LightGBM Classifier**) was trained to determine the key drivers of a trade's profitability (i.e., will a trade result in a profit or a loss?).
  * **SHAP (SHapley Additive exPlanations)**, a state-of-the-art model explainability technique, was used to quantify the precise impact of each feature (e.g., trade size, market sentiment, time of day) on the model's predictions.

## Key Findings & Visualizations

The analysis yielded several key insights, supported by the visualizations found in the `outputs/` directory.

  * **Contrarian Market Behavior:** The initial EDA revealed that traders make larger-sized trades during 'Fear' but that overall selling pressure increases during 'Greed', suggesting a broad "buy the fear, sell the greed" pattern.

      * *(see `outputs/time_series_volume_vs_sentiment.png`)*

  * **Discovery of Trader Personas:** Four distinct trader personas were identified through clustering, each with a unique trading style.

      * **High-Volume Momentum Whales:** High-capital traders who are most active and profitable during 'Greed'.
      * **Cautious Contrarians:** Highly effective traders with a high win rate who primarily trade during 'Fear'.
      * **Low-Impact Retail:** Infrequent traders with low volume and negligible PnL.
      * **Active Scalpers:** High-frequency traders with low profitability per trade.
      * *(see `outputs/trader_persona_radar_chart.png`)*

  * **Persona-Based Performance:** The analysis confirmed that different personas excel in different market conditions. The "Contrarians" were the only group consistently profitable during 'Fear', highlighting that no single strategy is optimal for all market states.

      * *(see `outputs/pnl_distribution_ridgeline_plot.png`)*

  * **Drivers of Profitability:** The SHAP analysis identified the most significant factors in predicting a profitable trade. Trade size (`size_usd`), market sentiment (`sentiment_value`), and starting position size (`start_position`) were among the top predictors.

      * *(see `outputs/shap_summary_dot_plot.png`)*

## How to Run the Code

1.  **Environment:** The primary analysis was conducted in a **Google Colab notebook**.
2.  **Requirements:** The key Python libraries used are listed in the first cell of the notebook, including `pandas`, `scikit-learn`, `lightgbm`, and `shap`.
3.  **Setup:**
      * Open `notebook_1.ipynb` in Google Colab.
      * Upload the two data files (`historical_data.csv` and `fear_greed_index.csv`) to the root directory of your Colab session.
4.  **Execution:** Run the notebook cells sequentially from top to bottom. The code is designed to load the data, perform all analyses, and generate all visualizations in order.

## Author

  * **Shreyas N**