# Multi-Omics Regulatory Network Analysis
### Integrative study of transcriptional and epigenetic regulation across five cancers using TCGA expression, DNA methylation, and ENCODE transcription factors.

This repository implements a workflow for integrative analysis of regulatory networks centred on long non-coding RNA (lncRNA) expression in cancer. Focusing on MIR100HG, the pipeline combines RNA-seq expression (TCGA), DNA methylation profiles (Illumina 450K), and curated transcription factor (TF) interactions (ENCODE). It comprises (i) stratification of tumour and normal cohorts into High/Low MIR100HG groups; (ii) differential expression analysis with Welch’s t-tests and Benjamini–Hochberg correction; (iii) promoter methylation–expression correlation analysis; (iv) TF prioritisation via Welch’s tests and Random Forest models; (v) PCA for dimensionality reduction and visualisation; and (vi) a BFS-based network module to classify TFs as direct or indirect regulators.

## Project Goal
The project is designed to characterise the transcriptional and epigenetic landscape of MIR100HG across pancreatic, lung, skin, prostate, and stomach cancers. By integrating multi-omics datasets, it identifies promoter methylation effects, prioritises key TFs (e.g. FOXP2, STAT3, GATA3), and reveals cancer-specific versus cross-cancer regulatory patterns. The workflow provides a reproducible framework for assessing lncRNA-centred networks and their role in tumour biology.

## Highlights
- **End-to-end pipeline**: cohort harmonisation → expression-based subgrouping → differential expression and methylation analysis → TF feature selection → PCA → network module.
- **Multi-omics integration**: TCGA RNA-seq, Illumina 450K DNA methylation, and ENCODE TF–target annotations combined into cancer-specific data matrices.
- **TF prioritisation**: Welch’s t-test across subgroups and Random Forest importance scoring (PAAD case study).
- **Network analysis**: breadth-first search to classify TFs as direct, indirect, or unreachable regulators relative to MIR100HG.
- **Visualisation**: correlation heatmaps, volcano plots, cross-tissue TF log2FC heatmaps, and PCA scatterplots.

## Analysis Framework
### 1) Expression and Subgrouping
- Samples stratified into High/Low MIR100HG groups using quantile thresholds (top/bottom 33% for main analysis).
- Tumour and normal cohorts harmonised to dominant histological subtypes for consistency.

### 2) Methylation Correlation
- Promoter CpG probes mapped from Illumina 450K arrays.
- Pearson correlation with MIR100HG expression, FDR-controlled, retaining negatively correlated probes (ri < –0.2, FDR < 0.05).

### 3) TF Expression and Prioritisation
- Differential expression tested via Welch’s t-test with BH correction.
- For PAAD, a Random Forest classifier ranked TF importance in discriminating High vs. Low MIR100HG.

### 4) PCA and Network Analysis
- Principal Component Analysis on TF expression, promoter methylation, and gender metadata to visualise subgroup separation.
- BFS traversal on curated TF–target networks to classify regulators by shortest path distance to MIR100HG.

## Case Studies
Findings include promoter hypermethylation repressing MIR100HG in PAAD, cancer-specific shifts in regulatory TFs (e.g. PBX3, FOXP2, STAT3), and convergent cross-cancer upregulation of FOXP2 and GATA3. These results highlight both context-specific and shared regulatory architectures of MIR100HG.

## References
- Uszczynska-Ratajczak *et al.* (2018). *Towards a complete map of the human lncRNA transcriptome.* Nat. Rev. Genet.  
- Papoutsoglou *et al.* (2021). *The noncoding MIR100HG RNA enhances autocrine TGF-β signalling.* Oncogene.  
- Cui *et al.* (2023). *The prognostic role of lncRNA MIR100HG across cancers.* Front. Genet.  
- Ottaviani *et al.* (2018). *TGF-β induces miR-100 and miR-125b controlling PDAC progression.* Cell Death Dis.  
- Li *et al.* (2021). *FOXP2 promotes progression of pancreatic cancer via lncRNA regulation.* Mol. Cancer.  
- Glass *et al.* (2013). *Passing messages between biological networks to refine interactions.* PLoS ONE.  

---

> Repository maintained by [DearKarl](https://github.com/DearKarl). Contributions and feedback welcome.
