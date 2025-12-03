**Astronomical Object Classification Using SDSS Photometry**

This project builds a complete data-mining pipeline for classifying astronomical objects (Stars, Galaxies, and QSOs) using only photometric data from the Sloan Digital Sky Survey (SDSS). Using machine learning models, feature selection, and unsupervised clustering, the system achieves up to 97.65% accuracy, demonstrating that photometric classification can effectively approximate spectroscopic labeling at large scale.

For full methodology, figures, experiments, and discussion, see the complete report: Astronomical Object Classification Using SDSS Photometry.pdf

**Overview**

Modern sky surveys produce massive photometric datasets. Spectroscopic labeling is accurate but expensive; photometric classification is fast but requires strong ML models. This project explores whether purely photometric and morphological features can reliably classify objects into:

- STAR
- GALAXY
- QSO (Quasi-Stellar Object)

The workflow includes:

- Dataset inspection & preprocessing
- Exploratory data analysis
- Univariate feature selection
- Supervised ML modeling
- Unsupervised clustering
- Cross-validation evaluation

**Insights & limitations**

Figure: Correlation Heatmap (Recommended)

<img width="755" height="678" alt="Screenshot 2025-12-03 at 15 15 47" src="https://github.com/user-attachments/assets/43a4b536-9e82-45af-9208-670d33f4ecff" />


This heatmap shows strong correlations among adjacent photometric bands and highlights feature relationships.


Figure: PCA Projection (K-Means Clusters)

<img width="851" height="698" alt="Screenshot 2025-12-03 at 15 16 34" src="https://github.com/user-attachments/assets/3615d2c0-50ff-49ba-825d-25cdfc5e06e8" />


**Dataset Description**

Dataset: SDSS Star/Galaxy/QSO photometry (100,000 samples)

Features include:

- u, g, r, i, z magnitudes
- Redshift
- Sky position: alpha (RA), delta (Dec)
- Derived color indices (e.g., g–r, r–i)
- SDSS identifiers (dropped during preprocessing)

Classes are nearly balanced:

- STAR: 33.1%
- GALAXY: 36.2%
- QSO: 30.7%


**Preprocessing Steps**

- Dropped non-predictive identifiers
- Encoded class labels (0, 1, 2)
- Standardized all numerical features
- Added derived features (color indices)
- Verified no missing values

**Exploratory Data Analysis (EDA)**

EDA included:

- Distribution of magnitudes
- Color index separation
- Correlation analysis
- Class distribution
- Redshift trends

Key insight: QSOs exhibit extreme photometric profiles and higher variance, while Stars are tightly clustered around near-zero redshift.

**Feature Selection**

Used ANOVA F-test to identify the top 10 most predictive features.

Most influential:

- u, g, r, i, z magnitudes
- Redshift
- Color indices: g–r, r–i, u–g

This reduced dimensionality while improving model efficiency.

**Supervised Machine Learning Models**

Four classifiers were trained using 10-fold cross-validation:

| Model             | Accuracy | Precision | Recall |
|-------------------|:--------:|:---------:|:------:|
| k-NN              | 92.82%   | 93.40%    | 90.63% |
| Decision Tree     | 96.17%   | 95.55%    | 95.63% |
| Random Forest     | 97.65%   | 97.76%    | 96.77% |
| Gradient Boosting | 97.45%   | 97.52%    | 96.57% |

Random Forest achieved the best performance, especially on QSO identification.


**Unsupervised Clustering**

Used to explore latent structure without labels:

_K-Means (k=3)_

- Reasonable cluster separation
- Some overlap between Galaxy & QSO

_Hierarchical Clustering_

- Clear STAR groupings
- More diffuse GALAXY / QSO clusters

_DBSCAN_

- Excellent for detecting anomalies
- Identified outliers among QSOs

**Insights & Discussion**

Key findings:

- Redshift is the single strongest predictor.
- Color indices are essential for separating QSOs.
- Photometric-only classification is viable at scale.
- Ensemble methods (RF, GBM) outperform simpler models.

**Limitations**

- Assumes clean, calibrated SDSS magnitudes
- Sensitive to high-redshift outliers
- Photometric uncertainty not modeled
- Clustering less effective for overlapping classes

**Authors**

Baker Huseyin

Islah Haoues
