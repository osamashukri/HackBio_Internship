<!--StartFragment-->

**Authors**: Pooja Solanki (@poojasolanki2024), Mahima Chakraborty (@mahima\_ch), Mariam Mohamed (@Mariam000v), Nourhan Saad (@Nourhan-25), Mercy Ade Ige (@MaiStar), Osama Shukri (@Osama), Tamosree Sikder (@Tamosree).

**Introduction**

Colon adenocarcinoma (COAD) is the most common colon cancer, it originates from mucus-producing glandular cells in the inner surface of the colon. These cells are responsible for producing mucus and other secretions that facilitate digestion. Diagnosis is confirmed via colonoscopy with biopsy. Adenocarcinoma typically develops over several years, often starting as a benign growth known as a polyp, which gradually becomes cancerous through genetic mutations and abnormal cell growth. 

**Methodology**

The key steps included data retrieval, preprocessing, normalization, differential expression analysis, visualization, functional enrichment analysis and machine learning analysis. 

- **Data sets**

RNA-Seq data for colon adenocarcinoma (COAD) were obtained from the Genomic Data Commons using the TCGAbiolinks R package. Only samples processed with the STAR alignment algorithm ("STAR - Counts") were included for consistency. A total of 40 samples (20 tumor, 20 normal) were selected for differential expression analysis, and the data were stored in CSV format for further analysis.

- **Data Preprocessing and Normalization**

The preprocessing stage involved aligning RNA-Seq count data (coad\_matrix) with metadata by matching sample identifiers. The data was then normalized using the TCGAanalyze\_Normalization function to account for gene length and sequencing depth, followed by filtering lowly expressed genes using the TCGAanalyze\_Filtering function, based on a quantile cutoff of 0.25. Finally, the data was log2-transformed for variance stabilization, and separate matrices for tumor and normal samples were generated for further analysis.

- **Differential expression analysis of individual genes**

To identify differentially expressed genes (DEGs) between tumor and normal tissue, the processed RNA-Seq data was analyzed using the TCGAanalyze\_DEA function from TCGAbiolinks. Expression levels were compared with the edgeR pipeline, applying a False Discovery Rate (FDR) cutoff of 0.01 and log2 fold-change (logFC) cutoff of 2. Differentially expressed genes (DEGs) were categorized as upregulated (logFC > 2) or downregulated (logFC < -2).

- **Functional Enrichment Analysis**

In this part, first, the **biomaRT** package was installed and we used the **useMart()** function to get the genes names. Then we used the **TCGAanalyze\_EAcomplete** function from the TCGAbiolinks package to perform the functional enrichment analysis for the upregulated and the downregulated genes. Then we used the visualization code **TCGAvisualize\_EAbarplot** to display the multiple enriched pathways for upregulated and the downregulated genes for multiple databases. 

- **Machine Learning Analysis** 

Feature selection involved choosing the top 8000 variable genes based on standard deviation, removing genes with near-zero variation and high correlation, and centering the data. The dataset was split into training (80%) and testing (20%) sets. A Random Forest model was trained using cross-validation, achieving 83.3% accuracy in predicting sample types. The top 10 important genes were identified, and gene names were retrieved using the biomaRt package from the Ensembl database.

**Results and Interpretation**

- The **volcano plot** highlights genes with significant expression changes, with upregulated genes shown in red and downregulated ones in blue. Notable genes like ENSG00000183034 (upregulated) and ENSG00000167755 (downregulated) show both large fold changes and significant FDR values, suggesting potential roles in cancer progression.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfGYkBhj71_JEJmzG8Y1DYZ-wURGghH83XQULBlRDYMm_GbXD3fWv9Q_9ksDcCvLkbMxH6TnHB8FGso2KLNbM4bjfbg6CjlUO4ZzuUDH6P19qRpIYyDNJ37va1q4QNafK5lh3iBTBqVnBYG_9yqZRlUmOo?key=jiARwZONPxZNyFjvGHv6hw)

_Figure 1: Volcano plot_

- The **heatmap** further confirms the distinct expression patterns between tumor and normal samples, with clear clustering. Overall, these results highlight key genes that may serve as potential biomarkers or therapeutic targets in colorectal cancer.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdEYhDkJMI5bXBieFYcLVj1ItZZgSDoyk3uZxNsdjWNTdQbX1Psq19_kBOrDzWVit6RaxrygtU18smuU6Mc6jMxLtDrHtiJrf7Mu5Enxbhg1MkKqcE7iyCZh_yHy6CG0Ub4Zer9wJwyOMcF5zkBUFJwHNxN?key=jiARwZONPxZNyFjvGHv6hw)

_Figure 2: Sample cluster heatmap_ 

- **Enrichment Analysis of the Upregulated Genes**

1. Amine Transport

This essential process promotes cell growth, development and proliferation as polyamines promote growth-related genes and activate ion channels involved in cell signaling pathways. Dysregulation of polyamine metabolism has been observed in cancer, and it is believed to contribute to the prevention of apoptosis in cancer cells. Elevated levels of polyamines were linked to the enhancement of oncogenes through mTOR and RAS pathways. Thus, they are considered a potential therapeutic target  (Novita Sari et al., 2021).

2. Carboxylic acid transport

This process involves the transportation of (-COOH) containing molecules such as lactate or pyruvate across membranes, which is crucial for cellular respiration and metabolism. Highly active carboxylic acid transporters such as MCTs (monocarboxylate transporters) for lactate, were found as key facilitators for cancer growth and invasion, by increasing the extracellular acidity and preventing intracellular acidosis, thus modulating the tumor microenvironment to promote cancer proliferation. Therefore, they are targeted for cancer therapy (Payen et al., 2017)(Pérez-Tomás & Pérez-Guillén, 2020).

****![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd7ViW5uW7vGBWMcs9osDFPAScI0Luk6ZW4dkY1Q6PAoY_EqpEZJOj0LusCusFIccZxCbdTji-uxCJvK5_guwz7eTJb9UkFTPC5eMZNPiIdtiRmt278wfINxT8e4QGyPJ-4FjESiuJ9Zwb5SOPZd6yxdrxU?key=jiARwZONPxZNyFjvGHv6hw)****_Figure 3: Significantly upregulated genes enriched pathways._

- **Enrichment Analysis of the Downregulated Genes**

1. Keratinization

Keratins, intermediate filament proteins in epithelial cells, provide structural support and act as tissue-specific markers in various tumors. In colorectal cancer (CRC), keratins contribute to tumor progression, with keratin 8 (K8) playing a protective role in maintaining colonic epithelial integrity. K8 deficiency leads to inflammation, hyperplasia, and a higher risk of CRC, emphasizing its potential tumor-suppressive function.

2. Keratinocyte differentiation

Keratinocyte Growth Factor (KGF) and its receptor KGFR (FGFR2 IIIb) play essential roles in promoting epithelial cell proliferation and differentiation, including in the colon. In colorectal cancer, KGFR is expressed in many patients and helps maintain well-differentiated tumor types. However, reduced or absent KGFR expression is associated with increased tumor aggression, invasiveness, and poorer prognosis. This loss of KGFR may trigger the activation of more aggressive cancer pathways, making it a key factor in both tumor development and progression. Thus, KGFR can serve as a potential prognostic marker in colorectal cancer (Yoshino et al., 2005)(Kudo et al., 2007).

\


****![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfry7bfSK0JuKmHRhtfOMXmWS_ChBwxe8o3OVY48CSYgWtvkBiBtu73pRifBe0q5XJY4Uz5jt6_d3zD3RDPm8swoY9aAhKaEfemnVKZiepSsOONudHZIT3BE6RlE65Y9oz0FxG8HPrWadp8gFScgROOFFyT?key=jiARwZONPxZNyFjvGHv6hw)****

_Figure 4: Significantly downregulated genes enriched pathways._

**Conclusion and Future Directions for Research**

Notably, upregulated genes were linked to processes such as amine and carboxylic acid transport, both of which are implicated in cancer cell proliferation and survival. Downregulated genes, including those involved in keratinization and keratinocyte differentiation, are critical in maintaining the integrity of the colon epithelium and are potential tumor suppressors. Furthermore, the machine learning model, based on random forest analysis, achieved an 83.3% accuracy in classifying tumor and normal samples. This demonstrates the potential of combining biomarker discovery with machine learning to improve early detection and prognosis in colon cancer.

**For future research, it is essential to explore the following areas:**

- Therapeutic Targeting: Identified pathways such as amine and carboxylic acid transport should be further investigated for potential therapeutic targets, especially in designing drugs that inhibit key transporters involved in cancer progression. Conduct in vivo studies using keratin 8 knock-out models to further investigate its role in CRC development and progression. This research could reveal mechanistic pathways through which K8 influences epithelial integrity and tumor behavior..

- Machine Learning Model Optimization: Future studies can focus on refining the machine learning model, incorporating additional features such as patient demographics, and exploring other machine learning algorithms to improve classification accuracy. The combination of deep learning with multi-omics information can uncover latent patterns and pathways associated with COAD progression.

**References**

- American Society of Clinical Oncology. (2018, October 25). Colorectal cancer: Treatment options. https\://www\.cancer.net/cancer-types/colorectal-cancer/treatment-options

- Colaprico, A., et al. (2016). TCGAbiolinks: An R/Bioconductor package for integrative analysis of TCGA data. \*Nucleic Acids Research\*, 44(8), e71.

- Comprehensive R Archive Network (CRAN). (n.d.). CRAN: Package pheatmap. https\://cran.r-project.org/web/packages/pheatmap/index.html

- Differential expression analysis – Introduction to RNA-seq. (n.d.). Data Carpentry - Introduction to RNA-seq. https\://scienceparkstudygroup.github.io/rna-seq-lesson/06-differential-analysis/index.html 

- Embl-Ebi. (n.d.). Biological interpretation of gene expression data | Functional genomics II. https\://www\.ebi.ac.uk/training/online/courses/functional-genomics-ii-common-technologies-and-data-analysis-methods/biological-interpretation-of-gene-expression-data-2/

- Koch, C. M., Chiu, S. F., Akbarpour, M., Bharat, A., Ridge, K. M., Bartom, E. T., & Winter, D. R. (2018). A beginner's guide to analysis of RNA sequencing data. \*American Journal of Respiratory Cell and Molecular Biology\*, 59(2), 145–157. https\://doi.org/10.1165/rcmb.2017-0430TR

- Kirk, S., Lee, Y., Sadow, C. A., Levine, S., Roche, C., Bonaccio, E., & Filiippini, J. (2016). The Cancer Genome Atlas Colon Adenocarcinoma Collection (TCGA-COAD) (Version 3) \[Data set]. The Cancer Imaging Archive. https\://doi.org/10.7937/K9/TCIA.2016.HJJHBOXZ

- Kudo, M., Ishiwata, T., Nakazawa, N., Kawahara, K., Fujii, T., Teduka, K., & Naito, Z. (2007). Keratinocyte growth factor-transfection-stimulated adhesion of colorectal cancer cells to extracellular matrices. \*Experimental and Molecular Pathology\*. https\://doi.org/10.1016/j.yexmp.2007.07.001

- Lin, S. M., Du, P., Huber, W., & Kibbe, W. A. (2008). Model-based variance-stabilizing transformation for Illumina microarray data. \*Nucleic Acids Research\*, 36(2), e11. https\://doi.org/10.1093/nar/gkm1075

- McDermaid, A., Monier, B., Zhao, J., Liu, B., & Ma, Q. (2019). Interpretation of differential gene expression results of RNA-seq data: Review and integration. \*Briefings in Bioinformatics\*, 20(6), 2044–2054. https\://doi.org/10.1093/bib/bby067

- Mitsuhiro, K., Ishiwata, T., Watanabe, M., Komine, O., Shibuya, T., Tokunaga, A., & Naito, Z. (2005). Keratinocyte growth factor receptor expression in normal colorectal epithelial cells and differentiated type of colorectal cancer. \*Oncology Reports\*, 13, 247–252. https\://doi.org/10.3892/or.13.2.247

- National Cancer Institute. (2022, November 14). Colon cancer treatment (PDQ®)—Patient version. https\://www\.cancer.gov/types/colorectal/patient/colon-treatment-pdq#section/\_112 

- Novita Sari, I., Setiawan, T., Seock Kim, K., Toni Wijaya, Y., Won Cho, K., & Young Kwon, H. (2021). Metabolism and function of polyamines in cancer progression. \*Cancer Letters\*, 519, 91–104. https\://doi.org/10.1016/j.canlet.2021.06.020 

- Payen, V. L., Hsu, M. Y., Rädecke, K. S., Wyart, E., Vazeille, T., Bouzin, C., Porporato, P. E., & Sonveaux, P. (2017). Monocarboxylate transporter MCT1 promotes tumor metastasis independently of its activity as a lactate transporter. \*Cancer Research\*, 77(20), 5591–5601. https\://doi.org/10.1158/0008-5472.CAN-17-0764 

- Pérez-Tomás, R., & Pérez-Guillén, I. (2020). Lactate in the tumor microenvironment: An essential molecule in cancer progression and treatment. \*Cancers\*, 12(11), 3244. https\://doi.org/10.3390/cancers12113244

- Polari, L., Alam, C. M., Nyström, J. H., Heikkilä, T., Tayyab, M., Baghestani, S., & Toivola, D. M. (2020). Keratin intermediate filaments in the colon: Guardians of epithelial homeostasis. \*The International Journal of Biochemistry & Cell Biology\*. https\://doi.org/10.1016/j.biocel.2020.105878

- The Cancer Genome Atlas Research Network. (2012). Comprehensive molecular characterization of human colon and rectal cancer. \*Nature\*, 487(7407), 330–337. https\://doi.org/10.1038/nature11252

- Werner, S., Keller, L., & Pantel, K. (2019). Epithelial keratins: Biology and implications as diagnostic markers for liquid biopsies. \*Molecular Aspects of Medicine\*. https\://doi.org/10.1016/j.mam.2019.09.001

\
\
\


<!--EndFragment-->
