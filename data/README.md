# Data

Raw data are not committed to this repository (size and licensing). Download them and place them next to the notebooks.

## GEO datasets (public)

Download each **Series Matrix File** from the Gene Expression Omnibus:

| Accession | Disease | Platform | Used in |
| --- | --- | --- | --- |
| [GSE75214](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE75214) | IBD (ulcerative colitis, Crohn's disease) vs control | GPL6244 | Notebooks 01 and 02 |
| [GSE6791](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE6791) | Cervical cancer vs normal | GPL570 | Notebook 02 |
| [GSE9750](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE9750) | Cervical cancer vs normal | GPL96 | Notebook 02 |
| [GSE63514](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE63514) | Cervical cancer vs normal | GPL570 | Notebook 02 |
| [GSE67522](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE67522) | Cervical cancer vs normal | GPL10558 | Notebook 02 |

Expected file names: `<ACCESSION>_series_matrix.txt` (unzipped). Platform annotation files (GPL570, GPL96, GPL10558) are downloaded automatically by `GEOparse` in notebook 02.

## Breast cancer expression matrix

Notebook 01 uses `X_data_full.csv` (1,191 samples × 56,937 genes, raw counts) and `y_data_full.csv` (Tumor / Normal labels). These files were provided as course material and are not redistributed here.
