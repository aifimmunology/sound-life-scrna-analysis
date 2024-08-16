## Reference Labeling

In this series of notebooks, we apply labels from our `celltypist` models, detect doublets, filter based on QC criteria, then cluster L2 cell types to identify remaining cross-type doublets. We then perform review of each L3 cell type and apply final filtering and reassignment to generate a clean set of labels for the full dataset.

This analysis is often distributed based on groups of subjects or by cell type to enable parallel processing of analysis steps and distribution of cell type results to domain experts for review. Notebooks prefixed with the same number perform the same analysis step across these groups of subjects or cell types.

**Note**: Due to availability of `celltypist` models at the time of this analysis, the cell type label assignment using `celltypist` was carried out in two stages - first for broad and intermediate resolution models (02 series), and later for the high resolution models (08 series). These steps could all be carried out together up front (at stage 02) if all models are available.

### 02 Label Predictions with L1 and L2 models

These notebooks carry out cell type labeling using `celltypist` models generated from the AIFI Immune Health Atlas at broad and intermediate resolution (L1 and L2, respectively).

Analysis was divided across groups of subjects to enable paralellization of labeling on 4 HISE IDE instances:  
02a-Python_label_predictions_celltypist_L1-L2_BR1_Female.ipynb  
02b-Python_label_predictions_celltypist_L1-L2_BR1_Male.ipynb  
02c-Python_label_predictions_celltypist_L1-L2_BR2_Female.ipynb  
02d-Python_label_predictions_celltypist_L1-L2_BR1_Male.ipynb

### 03 Doublet detection

In this notebook, we utilized `scrublet` to perform a first pass of doublet detection. All samples were analyzed in a single notebook for this step:  
03-Python_doublet_detection.ipynb

### 04 Assembly of subsets

After type prediction and doublet detection, we assembled large `anndata` objects (stored in .h5ad format) for subsets of subjects based on cohort and biological sex. These subsets enabled handling of parts of the full dataset for QC filtering without loading the entire set into memory:  
04-Python_assembly_of_subsets.ipynb

### 05 QC filtering

After subsetting, we loaded in the groups of samples and filtered cells based on QC criteria:

1. Not detected as a doublet by scrublet
2. < 10% of UMIs were assigned to mitochondrial genes
3. More than 200 and less than 5,000 genes detected

Cells that passed these criteria were saved for further analysis.

### 06 Partitioning of cell classes

To review labels at the intermediate (L2) resolution, we clustered cells using the Leiden algorithm within each L2 cell type. Because this is very resource intensive for extremely large datasets, we partitioned abundant cell types by subject cohort and biological sex for review and filtering of potential doublets. Any cell type with > 1 million cells across all subjects was selected and subclustered within these subject groups for filtering in these notebooks:  
06a-Python_partition_large_cell_classes_BR1_Female.ipynb  
06b-Python_partition_large_cell_classes_BR1_Male.ipynb  
06c-Python_partition_large_cell_classes_BR2_Female.ipynb  
06d-Python_partition_large_cell_classes_BR2_Male.ipynb  

Cell types with < 1 million cells were assembled across all subject groups and clustered together for review in this notebook:  
06e-Python_partition_small_cell_classes.ipynb

### 07 Filtering cell classes

In this step, we apply filtering rules to remove clusters within each L2 cell type that contain cross-type doublets or low-quality cells. Threshholds for identifying doublets were assigned for each L2 cell type to account for variation in marker gene abundance. Clusters with low median gene detection were also removed as low quality cells.

Cells were filtered based on marker and gene detection criteria in this notebook:  
07-Python_filter_cell_classes.ipynb

As part of the clustering and filtering process, tables and UMAP projections were generated to identify and tabulate cells that were removed. This notebook was used to generate figures that could be used to review and adjust filtering criteria:  
07a-R_filter_review_plots.ipynb

### 08 Label predictions with L3 model

At this stage, we assigned cell type labels using our high resolution (L3) celltypist model. As noted above, this labeling could also be performed along with L1 and L2 at stage 02 in future analyses. These assignments were again performed on cohort and biological sex-partitioned samples for parallelization:
08a-Python_label_predictions_celltypist_L3_BR1_Female.ipynb  
08b-Python_label_predictions_celltypist_L3_BR1_Male.ipynb  
08c-Python_label_predictions_celltypist_L3_BR2_Female.ipynb  
08d-Python_label_predictions_celltypist_L3_BR2_Male.ipynb  

### 09 Partitioning of L3 cell types

After assigning L3 cell type labels, we assembled cells that were filtered in stage 07 from each L3 cell type across all samples:  
09-Python_partition_L3_data.ipynb

### 10 Clustering L3 cell types

Once partitioned into separate .h5ad files for each cell type, we performed Leiden clustering within each cell type in a separate notebook for each cell class. Analysis of sets of cell types per class allowed paralellization of this clustering step across multiple IDEs:  
10a-Python_cluster_L3_b_cell_data.ipynb  
10b-Python_cluster_L3_cd4_t_cell_data.ipynb  
10c-Python_cluster_L3_cd8_t_cell_data.ipynb  
10d-Python_cluster_L3_other_t_cell_data.ipynb  
10e-Python_cluster_L3_myeloid_cell_data.ipynb  
10f-Python_cluster_L3_nk_cell_data.ipynb  
10g-Python_cluster_L3_other_cell_data.ipynb

### 11 Review of L3 clustering results

After clustering, we visualized UMAP projections and marker gene expression for each L3 cell type. Review of these plots by our domain expert cell type assignment team identified remaining doublets and misassigned cell labels that were corrected in the final stage of labeling analysis.

These notebooks utilized the [Pretty Jupyter](https://pretty-jupyter.readthedocs.io/en/latest/) HTML report generation templates to provide reviewers with a convenient format for review of cell types. To generate these reports, we used:
```
jupyter nbconvert --to html --template pj <notebook>
```

The following notebooks were used for cell type review:  
11a-Python_review_L3_b_cell_data.ipynb  
11b-Python_review_L3_cd4_t_cell_data.ipynb  
11c-Python_review_L3_cd8_t_cell_data.ipynb  
11d-Python_review_L3_other_t_cell_data.ipynb  
11e-Python_review_L3_myeloid_data.ipynb  
11f-Python_review_L3_nk_data.ipynb  
11g-Python_review_L3_other_data.ipynb

### 12 Filtering of L3 results

After review, doublets and cell type reassignments were performed by identifying marker gene expression threshholds that could be used to select clusters. In these notebooks, we perform this selection and removal or reassignment, track the reason for each change, and recluster the filtered cells for a final round of review:  
12a-Python_filter_L3_b_cell_data.ipynb  
12b-Python_filter_L3_cd4_t_cell_data.ipynb  
12c-Python_filter_L3_cd8_t_cell_data.ipynb  
12d-Python_filter_L3_other_t_cell_data.ipynb  
12e-Python_filter_L3_myeloid_data.ipynb  
12f-Python_filter_L3_nk_data.ipynb  
12g-Python_filter_L3_other_data.ipynb

### 13 Final Review of L3 results

Finally, we generated an additional round of cell type review plots, including UMAP projections, clustering, and marker gene expression. If results in these notebooks revealed that adjustments needed to be made to our filtering criteria at stage 12, we adjusted the steps taken in stage 12 and regenerated final reviews:  
13a-Python_review_filtered_L3_b_cell_data.ipynb  
13b-Python_review_filtered_L3_cd4_t_cell_data.ipynb  
13c-Python_review_filtered_L3_cd8_t_cell_data.ipynb  
13d-Python_review_filtered_L3_other_t_cell_data.ipynb  
13e-Python_review_filtered_L3_myeloid_data.ipynb  
13f-Python_review_filtered_L3_nk_data.ipynb  
13g-Python_review_filtered_L3_other_data.ipynb
