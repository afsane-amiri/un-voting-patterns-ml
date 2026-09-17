# Geopolitical Blocs at the UN: Machine Learning Analysis of Voting Patterns

A machine learning analysis of United Nations General Assembly (UNGA) voting records to identify geopolitical voting blocs, examine how those blocs evolve and deviate across issues, and investigate whether international voting patterns can predict Canada's voting behaviour.

This project was completed as a **team project for SCS3523 Machine Learning** at the University of Toronto School of Continuing Studies.

## Research Questions

The project investigates three main questions:

1. **Do geopolitical voting blocs exist and persist?**
   Can unsupervised learning identify stable voting coalitions among UN member states, and do countries remain within those coalitions over time?

2. **What causes countries to deviate from their blocs?**
   Which issues generate the greatest disagreement within voting blocs, and which countries behave most independently?

3. **Can geopolitical voting patterns predict Canada's vote?**
   Can the voting behaviour of other countries be used to predict how Canada votes on UN resolutions?

## Dataset

The analysis uses **United Nations General Assembly voting records**, covering resolutions from December 1946 through December 2025.

Each observation represents a country's vote on a resolution, with votes recorded as:

* **Y** — Yes
* **N** — No
* **A** — Abstain
* **X** — Absent

Resolutions also contain subject classifications such as human rights, nuclear disarmament, and the Palestine question, enabling voting behaviour to be examined across geopolitical issue areas.

For the primary clustering analysis, the data is filtered to **2000 onward** to represent the modern post-Cold War international structure. A separate temporal analysis extends back to **1980** to study changes in voting alignment over time.

**Source:** United Nations Digital Library

> The raw dataset is approximately 348 MB and therefore is not stored directly in this repository. See [`data/README.md`](data/README.md) for setup instructions.

## Methodology

### Data Preparation

The preprocessing pipeline includes:

* filtering the voting records by time period;
* standardizing country names;
* removing obsolete or historical states;
* encoding categorical UN votes numerically;
* processing multi-label resolution subjects; and
* handling missing values.

### Unsupervised Learning

Country voting behaviour is transformed into a country-topic feature matrix and analyzed using:

* **K-Means clustering**
* **Agglomerative clustering**
* **DBSCAN**
* **Principal Component Analysis (PCA)** for dimensionality reduction and visualization
* **Silhouette score and inertia** for cluster evaluation

Cluster selection is performed in the original standardized feature space, while PCA is primarily used for visualization and robustness analysis.

### Geopolitical and Temporal Analysis

The identified clusters are further examined using:

* within-cluster voting variance;
* topic-level disagreement;
* cluster transition matrices;
* longitudinal voting patterns; and
* cosine similarity between countries and geopolitical groups.

The analysis explores whether geopolitical voting blocs persist over time and which issues create the greatest deviations from bloc-level behaviour.

### Predictive Modelling

The project also applies supervised machine learning to voting behaviour.

Models and techniques include:

* Logistic Regression
* Random Forest
* Decision Tree
* Truncated SVD embeddings
* Leave-one-out evaluation

One application uses historical UNGA voting behaviour to model how countries might align on a security-related resolution.

A separate case study examines whether other countries' voting patterns can predict **Canada's UN voting behaviour** and how consistently Canada follows its broader geopolitical bloc.

## Key Findings

The analysis found meaningful structure in international UN voting behaviour.

Although a two-cluster K-Means solution achieved the strongest silhouette score, a **three-cluster solution provided greater geopolitical interpretability**, representing broadly Western-aligned, alternative/opposing-alignment, and mixed/non-aligned voting patterns.

DBSCAN did not produce meaningful density-separated groups in the high-dimensional voting space, suggesting that UN voting alignment behaves more like a continuous similarity structure than a set of compact density clusters.

The temporal analysis also found substantial persistence in geopolitical voting alignment across decades, while topic-level analysis revealed that certain issues generate considerably more within-bloc disagreement than others.

In the project's external predictive application, the **human-rights-based model achieved the strongest performance among the tested thematic models**, correctly predicting 14 of 15 observed Security Council votes in the evaluation.

The Canada case study further examines where Canadian voting behaviour follows or departs from its broader geopolitical alignment.

## Repository Structure

```text
Machine-Learning/
│
├── README.md
├── un-voting-patterns-machine-learning.ipynb
├── requirements.txt
├── .gitignore
│
├── data/
│   └── README.md
│
└── outputs/
    └── generated model outputs
```

## Running the Project

Clone the repository:

```bash
git clone https://github.com/afsane-amiri/Machine-Learning.git
cd Machine-Learning
```

Install the required Python packages:

```bash
pip install -r requirements.txt
```

Obtain the voting dataset described in [`data/README.md`](data/README.md) and place it at:

```text
data/2026_02_06_ga_voting.csv
```

Then open:

```text
un-voting-patterns-machine-learning.ipynb
```

and run the notebook cells in order.

Generated prediction files are written to the `outputs/` directory.

## Technologies

**Python · pandas · NumPy · scikit-learn · SciPy · Matplotlib · Seaborn · Statsmodels · Jupyter Notebook**

## Team

This project was completed collaboratively for **SCS3523 Machine Learning**.

**Team members:** Jiahui Song, Manasi Kanade, Afsane Amiri, Bobbie Williams, and Myriam Dilindi.

The repository preserves the collaborative nature of the original coursework while presenting the analysis and methodology as a reproducible machine learning project.

## Data Source

United Nations General Assembly voting records are available through the **United Nations Digital Library**.
