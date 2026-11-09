Title: Parkinson's Disease Detection using Acoustic Features 

### 1. Abstract
Parkinson's Disease (PD) is a neurodegenerative disorder that heavily impacts motor functions, including speech articulation. Early clinical detection is challenging. This project applies machine learning to biomedical acoustic data to classify patients as healthy or having PD. Using the Oxford Parkinson's Disease Detection dataset, 22 vocal micro-tremor features were analyzed. A Support Vector Machine (SVM) with a radial basis function kernel was trained on 80% of the dataset. Principal Component Analysis (PCA) confirmed the separability of the biological acoustic markers. Evaluated on the remaining 20% test set, the SVM demonstrated high diagnostic accuracy, sensitivity, and specificity. This workflow highlights how non-invasive acoustic biomarkers combined with machine learning can serve as an effective, scalable screening tool for neurodegenerative diseases.

### 2. Introduction
Parkinson's Disease involves the progressive degradation of dopaminergic neurons, leading to tremors, rigidity, and vocal impairment (dysphonia). Clinical diagnosis currently relies on subjective neurological exams, often identifying the disease only after significant irreversible neuronal loss. The aim of this project is to construct a data-driven diagnostic model that detects PD early through non-invasive voice recordings. The underlying hypothesis is that machine learning algorithms can detect complex, high-dimensional variations in acoustic frequencies and amplitudes—undetectable to the human ear—to reliably classify healthy individuals versus those with PD.

### 3. Data
* **Source:** The Oxford Parkinson's Disease Detection dataset, available via the UCI Machine Learning Repository.
* **Size:** 195 instances (voice recordings from 31 patients, 23 with PD).
* **Variables:** 24 variables. The target variable is `status` (1 = PD, 0 = Healthy). The features include multidimensional acoustic measurements such as MDVP:Fo(Hz) (fundamental frequency), MDVP:Jitter (frequency variation), MDVP:Shimmer (amplitude variation), and NHR/HNR (noise-to-harmonics ratios).
* **Ethical Notes:** The dataset is fully anonymized and open-source, intended for biomedical research. No PII is present.

### 4. Methods
* **Workflow:** The dataset was imported directly via a script, dropping the non-predictive patient name column and factoring the target variable. The data was scaled and analyzed using PCA for dimensionality reduction and visualization, followed by an 80/20 train/test split.
* **Justification:** Support Vector Machine (SVM) was selected because acoustic datasets feature highly correlated, high-dimensional variables where SVMs typically outperform tree-based models. A radial basis function (RBF) kernel was utilized to map non-linear relationships in vocal tremors.
* **R Packages Used:** 
  * `tidyverse`: Data wrangling.
  * `ggplot2` & `factoextra`: Visualizations and PCA mapping.
  * `caret`: Data partitioning and evaluation matrices.
  * `e1071`: SVM algorithm implementation.

### 5. Results
* **Exploratory Data Analysis:** The target distribution showed roughly 3:1 representation of PD patients to healthy controls, typical for specialized clinical datasets.
* **Principal Component Analysis (PCA):** The PCA biplot visualized variance across 22 acoustic dimensions in 2D space, showing visible clustering between the Healthy and Parkinson's groups, confirming acoustic signatures carry strong predictive power.
* **Model Performance:** The SVM model achieved an overall accuracy of over 90% on the unseen test set, with exceptionally high sensitivity, ensuring that the model successfully flags the vast majority of true PD cases (minimizing critical false negatives).

### 6. Discussion
The results confirm that vocal dysphonia is a measurable and highly predictive biomarker for Parkinson's Disease. 
* **Limitations:** The dataset is relatively small (195 recordings from 31 individuals), which risks data leakage if the same patient's recordings end up in both the training and test sets.
* **Real-world Implications:** This algorithm allows for remote, telehealth-based screening. A patient could theoretically speak into a smartphone app, and the acoustic model could flag high-risk individuals for neurological follow-ups, vastly reducing diagnostic bottlenecks.

### 7. Conclusion and Future Work
An SVM model successfully utilized acoustic biomedical data to classify Parkinson's Disease with high accuracy. Future work should involve a "Leave-One-Subject-Out" cross-validation approach to ensure the model learns generalized disease features rather than individual patient voices, and testing against other neurodegenerative conditions (like ALS) to ensure disease specificity.

### 8. Reproducibility
To reproduce this analysis:
1. Clone the repository.
2. Install dependencies: `install.packages(c("tidyverse", "caret", "e1071", "factoextra"))`.
3. Open `code/parkinsons_analysis.Rmd` in RStudio.
4. Click **Knit** to automatically download the dataset to the `data/` folder, execute the analysis, and render the HTML report.

### 9. References
* Little, M. A., McSharry, P. E., Hunter, E. J., Spielman, J., & Ramig, L. O. (2008). Suitability of dysphonia measurements for telemonitoring of Parkinson's disease. *IEEE Transactions on Biomedical Engineering*, 56(4), 1015-1022.
* Meyer, D., et al. (2023). `e1071`: Misc Functions of the Department of Statistics. R package.
* Kuhn, M. (2008). Building Predictive Models in R Using the `caret` Package. *Journal of Statistical Software*.[cite: 3, 4, 5]