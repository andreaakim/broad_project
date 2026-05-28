# Broad Project

This repository contains the analysis I performed on mouse phenotype ontology data using semantic embedding models. The main goal of this project was to compare how different embedding models represent biological phenotype terms and to identify where the models agree or disagree with the structure of the mouse phenotype ontology.

## Project Overview

Biological ontologies organize phenotype terms in a structured way, usually as a directed graph where broader biological concepts connect to more specific terms. In this project, I used the Mouse Phenotype Ontology as the reference structure and compared it against semantic embedding models that encode phenotype names as numerical vectors.

The purpose of this analysis was to see whether embedding models capture relationships that are similar to the ontology structure, and where they may differ. This is useful because embedding models can identify semantic similarity between terms, but they may not always follow the same biological hierarchy as the ontology.

## Main Goals

- Compare semantic embedding models on mouse phenotype terms
- Measure how closely embedding similarity matches ontology-based similarity
- Identify phenotype pairs that are semantically close in embedding space but far apart in the ontology
- Visualize phenotype embeddings using dimensionality reduction
- Compare clustering results across different embedding models
- Evaluate how well embedding-based trees match the ontology structure

## Data

The main dataset used in this project is the Mouse Phenotype Ontology. Phenotype IDs and phenotype names were extracted from the ontology and used for analysis.

Examples of ontology information used include:

- Mouse Phenotype IDs, such as `MP:0000001`
- Phenotype term names
- Parent-child relationships between ontology terms
- Ancestor relationships for each phenotype term

## Embedding Models

Several semantic embedding models were used to convert phenotype names into vector representations:

- MiniLM
- PubMedBERT
- BioLORD

These models were compared to see how differently they represent biological phenotype terms.

## Methods

### Ontology-Based Analysis

The ontology was represented as a graph using NetworkX. Ancestor relationships were used to describe the position of each phenotype term in the ontology. In some analyses, the ontology graph was converted to an undirected graph so that shortest-path distances could be calculated between terms.

Ontology-based comparisons included:

- Ancestor matrix construction
- Shortest-path distances
- Resnik similarity
- Pairwise ontology distance matrices

### Embedding-Based Analysis

Each phenotype name was embedded into a numerical vector using a semantic embedding model. Pairwise distances were then computed between embedded phenotype terms.

Embedding comparisons included:

- Cosine distance
- Euclidean distance
- Pairwise distance matrices
- Nearest-neighbor comparisons

### Correlation and Similarity Tests

To compare ontology structure with embedding structure, pairwise distance matrices were compared using:

- Spearman correlation
- Pearson correlation
- Mantel tests

These tests helped measure whether phenotype terms that are close in the ontology are also close in embedding space.

### Clustering

Clustering was used to compare how phenotype terms group together across different embedding models.

Clustering methods included:

- Leiden clustering
- HDBSCAN
- KMeans
- Gaussian Mixture Models

Cluster agreement was evaluated using metrics such as:

- Adjusted Mutual Information
- Jaccard similarity
- Cluster overlap heatmaps

### Tree-Based Comparisons

Hierarchical clustering was used to convert embedding distances into tree-like structures. These trees were then compared to ontology-based structures.

Tree comparison methods included:

- SciPy hierarchical clustering
- Dendrogram construction
- Cophenetic correlation
- Robinson-Foulds style comparison
- Tree edit distance

## Visualizations

This project includes visualizations to better understand how the embedding models organize phenotype terms.

Examples include:

- UMAP plots of phenotype embeddings
- UMAP plots colored by ontology branch
- Cluster heatmaps
- Dendrograms
- Highlighted ontology graphs showing disagreement pairs
- Plots comparing model distances and ontology distances

## Repository Structure

```text
.
├── analysis_notebooks/    # Jupyter notebooks for analysis
├── data/                  # Ontology files and processed data
├── environment.yml        # Conda environment file
├── requirements.txt       # pip environment backup
└── README.md              # Project description
```

The exact folder structure may vary depending on where the notebooks and data files are stored.

## Environment Setup

To create the Conda environment, run:

```bash
conda env create -f environment.yml
conda activate mouse-ontology-env
python -m ipykernel install --user --name mouse-ontology-env --display-name "Python (mouse-ontology-env)"
```

Then open Jupyter and select:

```text
Python (mouse-ontology-env)
```

as the notebook kernel.

If Conda does not work, the pip version can be installed using:

```bash
pip install -r requirements.txt
```

## Main Python Packages

This project uses:

- NumPy
- pandas
- SciPy
- scikit-learn
- NetworkX
- matplotlib
- seaborn
- UMAP
- HDBSCAN
- igraph
- leidenalg
- scikit-bio
- sentence-transformers
- transformers
- PyTorch
- zss

## How to Run the Notebooks

1. Create and activate the environment.
2. Open JupyterLab or Jupyter Notebook.
3. Select the `Python (mouse-ontology-env)` kernel.
4. Run the notebooks in order, starting with data loading and preprocessing.
5. Continue with embedding generation, distance calculations, clustering, and comparison analyses.

## Notes

Some analyses can require a large amount of memory because the ontology contains many phenotype terms. Pairwise distance matrices can become very large, especially when comparing all terms against each other. For larger analyses, it may be helpful to save intermediate files and avoid recomputing distance matrices.

## Summary

Overall, this project compares biological ontology structure with semantic embedding models to evaluate how well different models capture phenotype relationships. The results help show where embedding models align with the ontology and where they identify semantic similarities that are not directly reflected in the ontology hierarchy.
