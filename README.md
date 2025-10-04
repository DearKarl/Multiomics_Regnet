# Multi-Omics Regulatory Network Analysis  

Integrative study of transcriptional and epigenetic regulation of MIR100HG across five cancers (PAAD, LUAD, PRAD, SKCM, STAD) and their matched GTEx normal tissues.

## Overview

This repository provides an integrated Python pipeline for studying MIR100HG regulation across TCGA cancers (PAAD, LUAD, PRAD, SKCM, STAD) and GTEx tissues. The pipeline combines transcriptome and DNA methylation data to characterise transcriptional and epigenetic influences on MIR100HG. It employs statistical testing to identify differential expression and methylation–expression associations, and applies machine-learning methods such as Random Forests to prioritise transcription factors, PCA for integrative feature exploration, and network traversal to uncover regulatory pathways.

## Background  

Although most of the mammalian genome is transcribed, less than 2% encodes proteins, with the majority corresponding to non-coding RNAs (ncRNAs). Long ncRNAs (lncRNAs, >200 nucleotides) are increasingly recognised as regulators of cancer pathways and as potential biomarkers. The TGF-β pathway, which promotes epithelial-to-mesenchymal transition (EMT), stemness, and metastasis in advanced cancer, has been linked to MIR100HG, a lncRNA upregulated in pancreatic ductal adenocarcinoma (PDAC) compared with normal tissues (TCGA vs GTEx). Epigenetic mechanisms such as DNA methylation further influence gene expression, and interactions among transcription factors, DNMTs, and lncRNAs provide additional regulatory complexity.

Traditional approaches to studying lncRNA regulation often consider gene expression or DNA methylation in isolation, yet the regulation of MIR100HG emerges from the interplay of transcription factors, DNA methylation, and lncRNA-mediated feedback. To address this complexity, this study applies machine learning techniques to integrate transcriptomic, epigenetic, and regulatory network data. This multi-layer approach enables the capture of non-linear interactions, the identification of molecular subgroups across cancer and normal tissues, and the prioritisation of transcription factors most strongly associated with MIR100HG activity.

## Project Goal  

This project aims to predict the regulatory role of MIR100HG using patient data from five cancers (PAAD, LUAD, SKCM, PRAD, STAD) and their corresponding normal tissues. Specifically, it:
1. Integrates transcription factor–target associations, DNA methylation, and gene expression from TCGA cohorts stratified by high and low MIR100HG expression. 
2. Combines transcription factor–target associations and gene expression from GTEx normal tissues to investigate baseline MIR100HG regulation.
3. Compares cancer and normal tissues to identify MIR100HG-associated features that are specific to malignant contexts.

## Key Analyses

- **Supervised Learning: Random Forest Classification**  
  - **Task**: Predict MIR100HG high/low expression states and prioritise transcription factors (TFs) that best explain subgroup membership across cancers and matched normal tissues.  
  - **Method**: Train Random Forest models on integrated features (TF expression, promoter methylation, and selected clinical covariates) and interpret global feature-importance profiles; compare rankings between cancer and normal to detect context shifts.  
  - **Output**: Reliable discrimination of MIR100HG subgroups and a concise, rank-ordered TF short‑list. In PAAD, normal pancreas emphasises MAX/RCOR1/NRF1, whereas tumours prioritise PBX3/FOXP2/STAT3; NR3C1 and TCF12 remain shared, highlighting candidate regulators for follow‑up.  

- **Differential Expression**  
  - **Task**: Identify TFs and targets associated with MIR100HG-high vs. MIR100HG-low states.  
  - **Method**: Quantile-based subgrouping, Welch’s t-tests with FDR control, and cross‑tissue aggregation.  
  - **Output**: Volcano tables/plots and cross‑tissue heat maps. Patterns reveal a strong normal–tumour shift (e.g., broad TF upregulation with high MIR100HG in normal pancreas versus attenuated or reversed effects in PAAD) and recurrent tumour‑specific upregulation of FOXP2 and GATA3 across multiple cancers.  

- **Dimensionality Reduction**  
  - **Task**: Summarise multi‑omics structure underlying MIR100HG phenotypes and visualise subgroup separation.  
  - **Method**: PCA on TF expression, promoter methylation, and clinical covariates; loading analysis to identify drivers of variance.  
  - **Output**: Partial separation of MIR100HG subgroups; promoter methylation loads negatively, TFs such as FOXP2 load positively, and clinical covariates (e.g., sex) contribute minimally—supporting a transcriptional/epigenetic axis linked to MIR100HG.  

- **Network Modelling**  
  - **Task**: Place candidate TFs within mechanistic routes leading to MIR100HG regulation.  
  - **Method**: Construct a directed TF–gene graph (ENCODE) and apply breadth‑first search to classify TFs as direct or indirect by shortest‑path distance; use network proximity to contextualise ML‑derived rankings.  
  - **Output**: Network‑aware prioritisation that highlights proximal regulators and plausible regulatory paths to MIR100HG, guiding experimental validation and hypothesis generation.  

## Data Sources  

- **Gene expression (cancer samples)**  
  - TPM (Transcripts Per Kilobase Million) gene expression levels were downloaded from:  
    [TCGA RNA-seq TPM](https://xenabrowser.net/datapages/?dataset=tcga_RSEM_gene_tpm&host=https%3A%2F%2Ftoil.xenahubs.net&removeHub=https%3A%2F%2Fxena.treehouse.gi.ucsc.edu%3A443).  
  - TPM values are provided as log2(TPM + 0.001).  
  - The data were split into separate files for each cancer type, with HGNC gene symbols added to each entry.  

- **TF–target associations**  
  - ENCODE Transcription Factor–Target datasets were downloaded from Harmonizome:  
    [ENCODE TF–Target associations](https://maayanlab.cloud/Harmonizome/dataset/ENCODE+Transcription+Factor+Targets).  
  - Additional files with different formats and processed genes are available at the same source.  

- **DNA methylation (450k array, Illumina HumanMethylation450 BeadChip)**  
  - Pancreatic cancer (PAAD): [TCGA.PAAD.sampleMap/HumanMethylation450](https://xenabrowser.net/datapages/?dataset=TCGA.PAAD.sampleMap%2FHumanMethylation450&host=https%3A%2F%2Ftcga.xenahubs.net&removeHub=https%3A%2F%2Fxena.treehouse.gi.ucsc.edu%3A443)  
  - Lung adenocarcinoma (LUAD): [TCGA.LUAD.sampleMap/HumanMethylation450](https://xenabrowser.net/datapages/?dataset=TCGA.LUAD.sampleMap%2FHumanMethylation450&host=https%3A%2F%2Ftcga.xenahubs.net&removeHub=https%3A%2F%2Fxena.treehouse.gi.ucsc.edu%3A443)  
  - Skin cutaneous melanoma (SKCM): [TCGA.SKCM.sampleMap/HumanMethylation450](https://xenabrowser.net/datapages/?dataset=TCGA.SKCM.sampleMap%2FHumanMethylation450&host=https%3A%2F%2Ftcga.xenahubs.net&removeHub=https%3A%2F%2Fxena.treehouse.gi.ucsc.edu%3A443)  
  - Prostate adenocarcinoma (PRAD): [TCGA.PRAD.sampleMap/HumanMethylation450](https://xenabrowser.net/datapages/?dataset=TCGA.PRAD.sampleMap%2FHumanMethylation450&host=https%3A%2F%2Ftcga.xenahubs.net&removeHub=https%3A%2F%2Fxena.treehouse.gi.ucsc.edu%3A443)  
  - Stomach adenocarcinoma (STAD): [TCGA.STAD.sampleMap/HumanMethylation450](https://xenabrowser.net/datapages/?dataset=TCGA.STAD.sampleMap%2FHumanMethylation450&host=https%3A%2F%2Ftcga.xenahubs.net&removeHub=https%3A%2F%2Fxena.treehouse.gi.ucsc.edu%3A443)  
  - ID/Gene mapping file: *probeMap_illuminaMethyl450_hg19_GPL16304_TCGAlegacy* downloaded from [Xena Browser](https://xenabrowser.net).  

- **Gene annotation**  
  - Genome reference: hg19 annotation file (*geneAnnotation_hg19_basicgenes.txt*).  
  - Downloaded using **annotatr** and **TxDb.Hsapiens.UCSC.hg19.knownGene** R packages.  
  - Includes details of gene regions such as promoters, exons, and 5′UTRs.  

- **Clinical information**  
  - File: *Survival_SupplementalTable_S1_20171025_xena_sp*  
  - Downloaded from:  
    [TCGA Pan-Cancer clinical tables](https://xenabrowser.net/datapages/?cohort=TCGA%20PanCancer%20(PANCAN)&removeHub=https%3A%2F%2Fxena.treehouse.gi.ucsc.edu%3A443).  
  - Contains metadata for all patients included in TCGA Pan-Cancer studies, not limited to the five cancers selected here.  

- **Gene expression (normal tissues)**  
  - Expression data from GTEx:  
    [GTEx RNA-seq TPM](https://xenabrowser.net/datapages/?dataset=gtex_rsem_isoform_tpm&host=https%3A%2F%2Ftoil.xenahubs.net&removeHub=https%3A%2F%2Fxena.treehouse.gi.ucsc.edu%3A443).  
  - HGNC gene symbols added to each entry.  

- **Phenotypes (normal tissues)**  
  - Phenotype data from GTEx:  
    [GTEx phenotype tables](https://xenabrowser.net/datapages/?dataset=GTEX_phenotype&host=https%3A%2F%2Ftoil.xenahubs.net&removeHub=https%3A%2F%2Fxena.treehouse.gi.ucsc.edu%3A443).  
  - Only phenotypes corresponding to the five selected tissues (pancreas, lung, prostate, skin, stomach) were used.  
  - GTEx sample ID format: `GTEX-[donor ID]-[tissue site ID]-SM-[aliquot ID]`.  

## Data Access
Due to size limitations, raw datasets are hosted on OneDrive:  
[🔗 Download Data (OneDrive)](https://1drv.ms/f/s!AtSPOuyiZcMKcT0YIUPQxLhIZEE?e=p1TSUE)

## References
- Consortium, E. P. *et al.* (2007). *Identification and analysis of functional elements in 1% of the human genome by the ENCODE pilot project.* **Nature**.  
- Uszczynska-Ratajczak *et al.* (2018). *Towards a complete map of the human lncRNA transcriptome.* **Nature Reviews Genetics**.  
- Nemeth *et al.* (2024). *Non-coding RNAs in disease: from mechanisms to therapeutics.* **Nature Reviews Molecular Cell Biology**.  
- Richardson *et al.* (2023). *Context-dependent TGF-β family signalling in cell fate regulation.* **Nature Reviews Molecular Cell Biology**.  
- Ottaviani *et al.* (2018). *TGF-β induces miR-100 and miR-125b but blocks let-7a through LIN28B controlling PDAC progression.* **Cell Death & Disease**.  
- Jin *et al.* (2012). *Linking DNA methyltransferases to epigenetic marks and nucleosome structure genome-wide in human tumour cells.* **Cell Research**.  
- Brenner *et al.* (2005). *Myc represses transcription through recruitment of DNA methyltransferase corepressor.* **Nature Genetics**.  
- Huang *et al.* (2022). *LncRNA-mediated DNA methylation: an emerging mechanism in cancer and beyond.* **Cell and Molecular Life Sciences**.  
- Papoutsoglou *et al.* (2021). *The noncoding MIR100HG RNA enhances autocrine function of transforming growth factor beta signalling.* **Oncogene**.  

---

> Repository maintained by [DearKarl](https://github.com/DearKarl). Contributions and feedback welcome.
