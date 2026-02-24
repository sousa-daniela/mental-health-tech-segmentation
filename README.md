# Mental Health in Tech — Employee Segmentation

**Author:** Daniela de Sousa Silva

## Description

This project applies unsupervised machine learning to identify distinct employee profiles from survey data on mental health experiences in the technology sector. The scenario mirrors a real-world HR context in which decision-makers must move beyond aggregate statistics to understand the different subgroups within their workforce and design targeted interventions accordingly.

The analysis uses the OSMI Mental Health in Tech Survey (2016), a publicly available dataset of 1,433 respondents across 63 questions. Due to licensing considerations, the original dataset is not included in this repository and must be downloaded separately.

The project follows a complete unsupervised learning pipeline, from exploratory analysis and data cleaning through feature engineering, dimensionality reduction, and clustering with cluster profiling and interpretation as the final output.

---

## Key Features

- **Data Cleaning Pipeline:** Gender normalisation from free-text input, age outlier handling, removal of redundant geographic and free-text columns, and consistent treatment of missing values.
- **Structural Missingness Handling:** Survey routing logic is identified and preserved, distinguishing between incidental non-response and structurally absent questions (e.g. employer-related items not applicable to self-employed respondents).
- **Feature Engineering:** Multi-label diagnosis fields parsed into binary indicators; ordered scales ordinally encoded to preserve ranking; high-cardinality country field collapsed; remaining categoricals one-hot encoded.
- **Dimensionality Reduction via PCA:** Components retained to explain 90% of total variance (95 components); 2-component projection produced separately for visualisation only.
- **Comparative Clustering:** K-Means, Agglomerative (Ward linkage), and DBSCAN applied and compared to ensure findings are not dependent on any single modelling assumption.
- **Quantitative Model Selection:** Elbow method, silhouette score, and Calinski-Harabasz score evaluated across k = 2–8; final k selection combines statistical criteria with interpretive and actionability arguments.
- **Cluster Profiling:** Cluster labels mapped back onto original (pre-encoded) survey responses for human-readable interpretation; heatmap visualisation of cluster characteristics.
- **Reproducibility:** Random seeds set throughout; all outputs saved to `outputs/`.

---

## Tech Stack

- **Language:** Python
- **Data Handling:** Pandas, NumPy
- **Modelling:** Scikit-learn, SciPy
- **Visualisation:** Matplotlib, Seaborn

---

## Project Structure

```
mental-health-tech-segmentation/
│
├── archive/
│   └── mental-heath-in-tech-2016_20161114.csv   # To be downloaded manually (not included)
│
├── outputs/
│   ├── 01_missing_map.png
│   ├── 02_demographics.png
│   ├── 03_pca_scree.png
│   ├── 04_pca_2d.png
│   ├── 05_elbow_silhouette.png
│   ├── 06_cluster_assignments.png
│   ├── 07_kmeans_comparison.png
│   ├── 08_dendrogram.png
│   ├── 09_cluster_profiles.png
│   └── processed_with_clusters.csv
│
├── pipeline.ipynb
├── requirements.txt
└── README.md
```

---

## Setup and Installation

### 1. Local Environment Setup

1. **Clone the Repository**

```
git clone https://github.com/sousa-daniela/mental-health-tech-segmentation.git
cd mental-health-tech-segmentation
```

2. **Create and Activate a Virtual Environment**

```
python3 -m venv venv
source venv/bin/activate
```

3. **Install Dependencies**

```
pip install -r requirements.txt
```

---

## Dataset Preparation

1. Download the **OSMI Mental Health in Tech Survey 2016** dataset from:
   - [Kaggle](https://www.kaggle.com/osmi/mental-health-in-tech-2016)

2. Extract the dataset and place the CSV file in the following location:

```
archive/mental-heath-in-tech-2016_20161114.csv
```

3. Ensure the file name matches exactly, as it is referenced directly in the notebook.

---

## Usage

1. Open the notebook:

```
pipeline.ipynb
```

2. Run the notebook sequentially from top to bottom to:

   - explore and visualise the raw data,
   - clean and standardise survey responses,
   - engineer features for machine learning,
   - reduce dimensionality using PCA,
   - fit and compare clustering algorithms,
   - profile and interpret the resulting employee segments.

All output figures and the processed dataset with cluster labels are automatically saved to `outputs/`.

---

## Methodological Notes

- Clustering is performed in an unsupervised, exploratory setting with no ground-truth labels. Cluster quality is assessed using multiple quantitative metrics (inertia, silhouette score, Calinski-Harabasz score) as well as qualitative inspection of cluster interpretability and actionability.
- The final number of clusters (k=3) is chosen over the statistically optimal k=2 on substantive grounds: the two-cluster solution recovers a structural artefact of the survey's routing logic rather than a psychologically meaningful segmentation. The choice of k=3 over k=4 is similarly justified. the four-cluster solution adds a gradation within an existing group rather than a qualitatively distinct profile warranting a different strategic response.
- PCA is used both for noise reduction (95-component space as clustering input) and for visualisation (2-component projection). These two uses are kept strictly separate throughout the notebook.
- DBSCAN is included as a diagnostic tool rather than a primary model, given its sensitivity to neighbourhood parameters in high-dimensional PCA-reduced space.

---

## Dataset Source

OSMI Mental Health in Tech Survey 2016 — Open Sourcing Mental Illness

[Kaggle](https://www.kaggle.com/osmi/mental-health-in-tech-2016)

---

## Author Notes

This project was developed as part of an unsupervised machine learning coursework assignment with an HR strategy framing. The emphasis is placed on methodological transparency, interpretability of results, and the practical actionability of the identified clusters for a non-technical audience.

---

## License

This project is licensed under the MIT License. See the LICENSE.md file for details.
