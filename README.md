# CryptoClustering

This repository contains a Jupyter Notebook (`Crypto_Clustering.ipynb`) that explores unsupervised learning techniques, specifically K-means clustering and Principal Component Analysis (PCA), to analyze cryptocurrency price changes.  The goal is to predict whether cryptocurrencies are more affected by 24-hour or 7-day price fluctuations.  The notebook includes data loading, preprocessing, model building, visualization, and analysis of results.  A detailed explanation of the code and choices made is provided in `Crypto_Clustering_ipynb_Explanation.pdf`.

## Repository Structure

```
CryptoClustering/
├── README.md                <- This file, providing an overview of the project.
├── Crypto_Clustering.ipynb  <- Jupyter Notebook with the main analysis code.
├── Crypto_Clustering_ipynb_Explanation.pdf <- PDF explaining the code and reasoning.
└── Resources/
    └── crypto_market_data.csv   <- CSV file containing the cryptocurrency data.
```

## Project Overview

This project leverages Python and unsupervised learning to analyze cryptocurrency price data.  The analysis proceeds in the following steps:

1.  **Data Loading and Preparation:**
    *   The `crypto_market_data.csv` file is loaded into a Pandas DataFrame.
    *   The data is preprocessed using `StandardScaler` from scikit-learn to normalize the numerical features.  This is crucial for K-means, as it is sensitive to feature scaling.
    *   The `coin_id` column is set as the DataFrame index.

2.  **Finding the Best Value for k (Elbow Method):**
    *   The Elbow method is used to determine the optimal number of clusters (k) for K-means clustering.  This involves calculating the inertia (sum of squared distances to the nearest cluster center) for different values of k (from 1 to 11).
    *   The inertia values are plotted against the corresponding k values, and the "elbow" point (where the rate of decrease in inertia slows down significantly) is identified as the optimal k.
    *   This process is performed both on the original scaled data and on the PCA-reduced data.

3.  **Clustering Cryptocurrencies with K-means:**
    *   K-means clustering is applied using the optimal k value determined in the previous step.
    *   The model is fit to the scaled data, and cluster assignments are predicted.
    *   The cluster assignments are added as a new column ('cluster') to the DataFrame.
    *   Scatter plots are generated using hvPlot to visualize the clusters, with cryptocurrencies colored according to their cluster assignments.  `hover_cols` are used to display the `coin_id` on hover.
    *   This is done both with the original scaled data and the PCA data.

4.  **Optimizing Clusters with Principal Component Analysis (PCA):**
    *   PCA is used to reduce the dimensionality of the data to three principal components.
    *   The explained variance ratio for each component is calculated and displayed, along with the total explained variance.
    *   A new DataFrame is created with the PCA-transformed data.

5.  **Finding the Best Value for k (Elbow Method) - PCA Data:**
    * The Elbow Method is applied *again*, but this time using the PCA-transformed data. This determines the best *k* value for use on the PCA data.

6.  **Clustering Cryptocurrencies with K-means - PCA Data:**
    *   K-means clustering is applied to the PCA-transformed data, using the optimal k value determined from the Elbow method *on the PCA data*.
    *   Cluster assignments are predicted and added to a copy of the PCA DataFrame.
    *   A scatter plot is created to visualize the clusters in the reduced-dimensional space (PC1 vs. PC2).

7. **Visualize and Compare the Results:**
    * Composite plots are generated using hvplot to facilitate direct comparison of the following:
        * The Elbow curves for the scaled data and the PCA data
        * The cluster assignments for the scaled data (original features) and the PCA data.

8. **Correlation Heatmap**
    *   A correlation heatmap is generated to show the correlation between the original features of the dataset, which aids in understanding the data prior to scaling, clustering, and dimensional reduction.

## Key Files and Explanations

*   **`Crypto_Clustering.ipynb`**: This Jupyter Notebook contains all the Python code for the analysis, including:
    *   **Importing Libraries:** Imports necessary libraries such as pandas, hvplot, scikit-learn (KMeans, PCA, StandardScaler), matplotlib, seaborn, and bokeh.
    *   **Data Loading:** Loads the `crypto_market_data.csv` file into a Pandas DataFrame.
    *   **Data Preparation:** Scales the data using `StandardScaler`.
    *   **Elbow Method Implementation:** Calculates and plots inertia for different k values.
    *   **K-means Clustering:** Fits and predicts cluster assignments.
    *   **PCA:** Performs dimensionality reduction.
    *   **Visualization:** Creates interactive plots using hvPlot and bokeh.  This includes scatter plots and the elbow curve plots.  Composite plots are used for direct comparison.
    *   **Answering Questions:** Provides answers to the questions posed in the original assignment instructions.

*   **`Crypto_Clustering_ipynb_Explanation.pdf`**:  This PDF document provides a detailed, step-by-step explanation of the code in the Jupyter Notebook.  It explains the purpose of each code block, the reasoning behind the chosen methods, and the interpretation of the results.  It also clarifies why certain parameters (like `n_init` in KMeans) are explicitly set.  It explains the importance of the correlation heatmap.

* **`crypto_market_data.csv`**: Contains the price change data for various cryptocurrencies across different time periods (24h, 7d, 14d, 30d, 60d, 200d, 1y). Each row represents a different cryptocurrency (`coin_id`).

## Dependencies

The project requires the following Python libraries:

*   pandas
*   hvplot
*   scikit-learn
*   matplotlib
*   seaborn
*   bokeh
*   holoviews

You can install these dependencies using pip:

```bash
pip install pandas hvplot scikit-learn matplotlib seaborn bokeh holoviews
```

## How to Run

1.  **Clone the Repository:**

    ```bash
    git clone https://github.com/AlexGerwer/CryptoClustering.git
    cd CryptoClustering
    ```
    
2.  **Install Dependencies:** (See the "Dependencies" section above.)

3.  **Open and Run the Notebook:**

    ```bash
    jupyter notebook Crypto_Clustering.ipynb
    ```

    This will open the Jupyter Notebook in your web browser.  Run all the cells sequentially to execute the analysis. The notebook includes markdown cells with explanations and visualizations. Read the `Crypto_Clustering_ipynb_Explanation.pdf` file for a detailed explanation.

## Key Findings

*   The optimal number of clusters (k) for both the original scaled data and the PCA-reduced data appears to be 4, based on the Elbow method.
*   Using PCA to reduce dimensionality results in tighter, more distinct clusters compared to using the original scaled data. This suggests that PCA effectively captures the most important variance in the data, leading to better cluster separation.
*   The total explained variance of the three principal components is approximately 89.5%, indicating that a significant portion of the original data's information is retained after dimensionality reduction.
*   The correlation heatmap helps identify features that are highly correlated, enabling informed decisions about feature selection or dimensionality reduction.

## License
The project is released under the MIT License, which is a permissive open-source license that allows users to freely use, modify, distribute, and sublicense the software with minimal restrictions. This means that anyone can incorporate this project into their own work, 
whether for personal, academic, or commercial purposes, as long as the original copyright notice and license terms are included. 
