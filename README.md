# MSCS 634 – Lab 3: Clustering Analysis Using K-Means and K-Medoids

## Purpose of the Lab

The goal of this lab was to practice clustering by applying K-Means and K-Medoids to the Wine dataset from scikit-learn. The dataset has 178 wine samples from 3 cultivars, with 13 chemical features each. I prepared and standardized the data, clustered it with k = 3 using both algorithms, evaluated the results with the Silhouette Score and the Adjusted Rand Index (ARI), and compared the two methods using plots and metrics.

## Files

- `MSCS_634_Lab_3_Clustering.ipynb`: the Jupyter Notebook with all code, outputs, plots and analysis
- `README.md`: this summary

## Results

| Algorithm | Silhouette Score | ARI | Correctly clustered |
|---|---|---|---|
| K-Means | 0.285 | 0.897 | 96.6% |
| K-Medoids | 0.268 | 0.741 | 91.0% |

## Key Insights

- **K-Means performed better** on both metrics. The silhouette scores were close, but K-Means had a much higher ARI, which means its clusters matched the real wine classes more closely.
- **Both models clustered `class_0` and `class_2` perfectly.** All the mistakes were `class_1` wines, which sit between the other two classes. K-Means got 6 of them wrong and K-Medoids got 16 wrong.
- **The difference comes from the cluster centers.** K-Means centers are averages and sit in the middle of each group. K-Medoids centers (medoids) have to be real data points. The `class_0` medoid was closer to the edge of its group, which moved the cluster border into the `class_1` area.
- **k = 3 was a good choice.** Besides matching the 3 classes, k = 3 also gave the highest silhouette score when I tested k = 2 to 8.
- **The silhouette scores were moderate (around 0.27–0.29).** This is normal for data with 13 features where the classes overlap a little.
- **When to use each:** K-Means works best for clean, numeric, scaled data and is faster on large datasets. K-Medoids is better when there are many outliers, when a different distance measure is needed, or when you want each cluster represented by a real example.

## Challenges and Decisions

- **Outliers:** the dataset had no missing values or duplicates, but about 10 rows had extreme values. I decided to keep them because they looked like real measurements, the dataset is small, and outlier handling is one of the main differences between the two algorithms.
- **Scaling:** the features had very different ranges (for example, proline goes up to 1680 while hue stays around 1), so I used z-score standardization so that every feature counts equally.
- **Fair comparison:** I used Euclidean distance for K-Medoids, the same as K-Means, so the difference in results comes from the algorithms and not the distance measure.
- **K-Medoids setup:** K-Medoids is not part of regular scikit-learn, so I installed the `scikit-learn-extra` package. I used the PAM method because it is the standard and more accurate version of K-Medoids.
- **Plotting 13 features:** I used PCA to reduce the data to 2 dimensions for the scatter plots only. Since cluster numbers are random, I matched each cluster to its closest class so the colors mean the same thing in both plots.

## How to Run

```bash
pip install numpy pandas matplotlib seaborn scikit-learn scikit-learn-extra jupyter
jupyter notebook MSCS_634_Lab_3_Clustering.ipynb
```
