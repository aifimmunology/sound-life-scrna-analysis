# Data Assembly

This set of notebooks is used to assemble our datasets for use in analysis after labeling, QC filtering, and refinement of labels.

### Assembly of data per sample

Here, we apply the labeling and filtering results from previous notebooks, and assemble data for each individual sample as a separate .h5ad file. This enables flexible use of data for each sample in downstream analyses:  
14-Python_assemble_data_per_sample.ipynb

### Assembly of cell type frequencies

This notebook is used to tabulate cell type frequency for each sample in our dataset. This is performed at each level of cell type resolution. We also compute proportions of cell types per sample, compute Centered Log Ratio (CLR) transformations for analysis, and normalize cell type abundance to clinical blood counts collected at the same time as blood draws for PBMCs:  
15-R_assemble_type_frequencies.ipynb

### Pseudobulk data assembly

Here, we generate Pseudobulk data by aggregating results for cells with the same high resolution (L3) cell type label within each sample. This aggregation is performed using multiple methods: summing UMI counts per gene (used for DESeq2 analysis), taking the mean of normalized and log transformed values (for visualization), and computing the number of cells in each group with gene detection (> 0; used for feature selection based on gene detection):  
16-R_assemble_pseudobulk_aggregate.ipynb

### Full Dataset UMAP

In this notebook, we performed UMAP projection on all cells in the full dataset. This takes a long time.  
17-Python_full_dataset_umap.ipynb

### Metadata Assembly

Here, we combine all relevant sample metadata for use in visualization tools.  
18-Python_assemble_complete_metadata.ipynb