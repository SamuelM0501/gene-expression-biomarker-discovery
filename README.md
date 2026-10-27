# Gene Expression Biomarker Discovery

Biomarker discovery from gene expression data across three diseases (breast cancer, inflammatory bowel disease and cervical cancer), comparing two strategies:

- **Statistical pipeline:** differential gene expression (Welch's t-test + Benjamini–Hochberg FDR), volcano plots, heatmaps and single-gene ROC/AUC, in the style of Rosati et al. (2024).
- **Machine-learning pipeline:** consensus feature selection with four methods (Mutual Information, RFECV, Elastic Net, Gradient Boosting) followed by classifier benchmarking, adapted from Syed et al. (2024).

The most engineering-heavy part of the project is the **cross-platform data integration**: four public GEO cervical-cancer studies from three different microarray platforms were mapped from probe IDs to gene symbols, harmonized to a common log2 scale and merged into a single 179-sample dataset.

## Notebooks

| Notebook | What it does |
| --- | --- |
| [`01_breast_cancer_biomarker_pipeline.ipynb`](notebooks/01_breast_cancer_biomarker_pipeline.ipynb) | ML pipeline on a breast cancer RNA-seq matrix (1,191 samples × 56,937 genes): DEG analysis, 4-method consensus feature selection, a 10-gene panel and 8 classifiers. |
| [`02_cross_cohort_ibd_cervical_validation.ipynb`](notebooks/02_cross_cohort_ibd_cervical_validation.ipynb) | **Part A:** statistical pipeline on the IBD cohort GSE75214, with weighted and boosted extreme learning machines for class imbalance. **Part B:** integration of four cervical-cancer GEO datasets and a head-to-head evaluation of both pipelines. |

## Key results

| Cohort | Samples | Finding |
| --- | --- | --- |
| Breast cancer | 1,191 (222 after balancing) | 7,224 differentially expressed genes; 10-gene consensus panel (MMP11, CA4, COL10A1, TSLP, VEGFD, …) |
| IBD (GSE75214) | 194 | 582 significant probes; best single probe AUC 0.97 (in-sample); boosted WELM reached 0.95 accuracy with 100% recall on the minority control class (validation split) |
| Cervical cancer (4 merged GEO studies) | 179 | 10,783 shared genes after probe-to-gene mapping; 321 DEGs; 5 genes (CDKN2A, KNTC1, NEK2, SMC4, SYCP2) selected by **both** pipelines |

Classification metrics in both notebooks are optimistic because of the limitations below. They are reported for transparency, not as expected real-world performance.

## Known limitations and roadmap

- [ ] **Data leakage:** in notebook 01, DEG analysis and feature selection use all samples before the train/test split; in notebook 02 Part B, the DEG candidate pool is computed before the split. Fix: move all gene selection inside the training folds (e.g. a scikit-learn `Pipeline` with cross-validation).
- [ ] **Batch effects:** the merged cervical dataset has no batch correction and a random split mixes studies. Planned: leave-one-dataset-out evaluation and a comparison with ComBat correction.
- [ ] **Small test sets:** replace single splits with repeated stratified cross-validation and report confidence intervals.
- [ ] **External validation for notebook 01:** apply the probe-to-gene mapping from notebook 02 so GSE75214 can actually be used as an external cohort.

## Data

Raw data are not stored in this repository. See [`data/README.md`](data/README.md) for how to obtain each dataset.

## Setup

```bash
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab
```

File paths in the notebooks are relative: place the data files in `notebooks/` next to the notebooks (and create `notebooks/outputs/` for notebook 01), or update the paths in the loading cells. Moving to a single `data/` folder is on the roadmap.

## Acknowledgements

This project started as coursework for DANA 4840 and DANA 4830 at Langara College and has been extended for this portfolio. The weighted and boosted ELM implementations in notebook 02 were adapted from an earlier team assignment.

**References**

- Syed et al. (2024). Machine-learning biomarker discovery pipeline (Figure 1A–B), used as the basis for the ML pipeline.
- Rosati et al. (2024). Bioinformatics biomarker identification for IBD on GSE75214, used as the basis for the statistical pipeline.
- Gene Expression Omnibus (GEO), NCBI: GSE75214, GSE6791, GSE9750, GSE63514, GSE67522.

## License

[MIT](LICENSE)
