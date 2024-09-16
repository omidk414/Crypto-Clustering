## Cryptocurrency Clustering Project

### Project Overview

This project utilizes unsupervised learning to predict if cryptocurrencies are affected by 24-hour or 7-day price changes. The process involves data normalization, clustering using K-means, and optimization with Principal Component Analysis (PCA).

### Table of Contents
- [Prepare the Data](#prepare-the-data)
- [Find the Best Value for k Using the Original Scaled DataFrame](#find-the-best-value-for-k-using-the-original-scaled-dataframe)
- [Cluster Cryptocurrencies with K-means Using the Original Scaled Data](#cluster-cryptocurrencies-with-k-means-using-the-original-scaled-data)
- [Optimize Clusters with Principal Component Analysis](#optimize-clusters-with-principal-component-analysis)
- [Find the Best Value for k Using the PCA Data](#find-the-best-value-for-k-using-the-pca-data)
- [Cluster Cryptocurrencies with K-means Using the PCA Data](#cluster-cryptocurrencies-with-k-means-using-the-pca-data)
- [Examples and Analysis](#examples-and-analysis)
- [Conclusion](#conclusion)
- [Acknowledgements](#acknowledgements)

---

### Prepare the Data

1. **Normalize the Data**: Use `StandardScaler()` from scikit-learn to normalize data from a CSV file.
2. **Create Scaled DataFrame**: Set "coin_id" as the index for the new DataFrame.

### Find the Best Value for k Using the Original Scaled DataFrame

1. **Elbow Method**:
   - Create a list of k values from 1 to 11.
   - Compute inertia for each k value.
   - Plot an elbow curve to identify the optimal k.

### Cluster Cryptocurrencies with K-means Using the Original Scaled Data

1. **K-means Clustering**:
   - Initialize and fit the model with the best k.
   - Predict clusters and add them to a copy of the original data.
   - Create a scatter plot using `hvPlot`.

### Optimize Clusters with Principal Component Analysis

1. **Perform PCA**:
   - Reduce features to three principal components.
   - Calculate explained variance: 0.3719856, 0.34700813, 0.17603793.

### Find the Best Value for k Using the PCA Data

1. **Elbow Method on PCA Data**:
   - Repeat steps similar to original data to find optimal k.

### Cluster Cryptocurrencies with K-means Using the PCA Data

1. **K-means Clustering on PCA**:
   - Predict clusters using PCA data and visualize using `hvPlot`.

### Examples and Analysis

# Elbow Curve for Original Scaled Data
```python

df_elbow.hvplot.line(x="k", y="inertia", title="Elbow Curve", xticks=best_k)
```
![Elbow1](https://github.com/omidk414/CryptoClustering/blob/main/images/elbow1.png)
The elbow curve suggests that an optimal value for k is around 4, where inertia starts to decrease at a slower rate.

# Crypto Clusters Scatter Plot
```python
crypto_plot = predictions_df.hvplot.scatter(
    x="price_change_percentage_24h",
    y="price_change_percentage_7d",
    by="clusters",
    hover_cols="coin_id",
    title="Crypto Clusters"
)
```
![Cluster1](https://github.com/omidk414/CryptoClustering/blob/main/images/cluster1.png)
The scatter plot shows distinct clusters of cryptocurrencies based on short-term and weekly price changes.

# Elbow Curve for PCA Data
```python
df_elbow.hvplot.line(x="k", y="inertia", title="Elbow Curve", xticks=k)
```
![Elbow2](https://github.com/omidk414/CryptoClustering/blob/main/images/elbow2.png)
The elbow curve for PCA data also suggests an optimal k value around 4, consistent with the original data findings.

# PCA Crypto Clusters Scatter Plot
```python
pca_plot = pca_predictions_df.hvplot.scatter(
    x="PC1",
    y="PC2",
    by="clusters",
    hover_cols="coin_id",
    title="Crypto Clusters"
)
```
![Cluster2](https://github.com/omidk414/CryptoClustering/blob/main/images/cluster2.png)
Using fewer features through PCA still provides clear clustering, indicating effective dimensionality reduction without significant loss of information. The total explained variance is approximately 89.5%, suggesting that most of the data's variability is captured by these components.

# Conclusion
Overall, by reducing the number of features impacts clustering performance using K-means. By comparing the clustering results from the original dataset and the PCA-transformed data, it highlights the effect of dimensionality reduction on the clustering process.

# Acknowledgements
Study Group Members:
    Gursimran Kaur - kaursimran081999@gmail.com - SimranBoparai
