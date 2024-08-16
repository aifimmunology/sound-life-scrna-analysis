# sound-life-scrna-analysis

This repository stores the steps used to generate the AIFI Sound Life cohort dataset based on 10x 3' scRNA-seq data. There are 4 major stages to this process. Each stage is stored in a subdirectory in this repository:

01-sample_selection: Sample selection and retrieval
02-reference_labeling: Labeling with the AIFI Immune Health Atlas CellTypist models
03-data-assembly: Assembly of data and labels for use in downstream analysis
04-file-sets: Notebooks used to build file sets for distribution of data on our website

The notebooks in sections 1-3 can be run sequentially based on their numeric prefix. They are also prefixed by the language/notebook kernel used in each (Python or R), as both languages are utilized in this analysis.

See the README.md files within each subdirectory for additional descriptions of the analysis notebooks.

## Contributors

#### Analysis

Qiuyu Gong: Analysis lead, composed most original notebook versions
Lucas Graybuck: Review, documentation, linting, and reproducibility management

#### Cell type annotation review

Marla Glass: B cell annotation lead
Claire Gustafson: Scientific lead; T cell annotation lead
Emma Kuan: Myeloid cell annotation lead
Tao Peng: NK cell annotation lead

<a id="legal_info"></a>

# Legal Information

<a id="license"></a>

## License

The license for this package is available on Github in the file LICENSE.txt in this repository.

<a id="support"></a>

## Level of Support

We are not currently supporting this code, but simply releasing it to the community AS IS but are not able to provide any guarantees of support. The community is welcome to submit issues, but you should not expect an active response.

<a id="contrib"></a>

## Contribution Agreement

If you contribute code to this repository through pull requests or other mechanisms, you are subject to the Allen Institute Contribution Agreement, which is available in the file CONTRIBUTING.md in this repository.
