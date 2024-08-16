## Sample selection and retrieval

### 00-R_Sample_Selection.ipynb
In this notebook, we query the HISE database to identify samples from healthy subjects. We use retrieve all samples available from two cohorts at the time of the analysis:  
BR1: Healthy adult samples from subjects 25-35 yr old; n = 47 subjects  
BR2: Healthy adult samples from subjects 55-65 yr old; n = 49 subjects

After selection, we store the metadata for these samples in HISE for downstream steps.

### 01-Python_retrieve_cmv_bmi.ipynb
In this notebook, we retrieve CMV infection status and compute BMI for each subject based on clinical lab data stored in HISE. We then store this data in HISE for downstream steps.
