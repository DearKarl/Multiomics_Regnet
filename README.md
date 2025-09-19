# Multi-Omics Regulatory Network Analysis  
### Integrative study of transcriptional and epigenetic regulation of MIR100HG across five cancers and matched normal tissues

## Background  
Despite most of the mammalian genome being transcribed to RNA, less than 2% encodes proteins, while the vast majority corresponds to non-coding RNAs (ncRNAs) [1]. High-throughput sequencing technologies have revealed thousands of long ncRNAs (lncRNAs, >200 nucleotides), yet only a small proportion has been functionally characterised [2]. LncRNAs have emerged as key regulators of cancer pathways and are considered promising biomarkers and therapeutic targets [3].  

The **TGF-β signalling pathway** plays a crucial role in cancer. In advanced stages, it acts as an oncogene promoting epithelial-to-mesenchymal transition (EMT), stemness, and metastasis [4]. Our laboratory has previously used RNA-seq to identify TGF-β-regulated lncRNAs in pancreatic ductal adenocarcinoma (PDAC) [5], selecting **MIR100HG** as a promising candidate due to its significant upregulation in cancer patients compared with healthy individuals (TCGA vs. GTEx). Preliminary evidence suggests MIR100HG is TGF-β regulated and may contribute to tumour development.  

In parallel, **DNA methylation** is a key epigenetic mechanism, catalysed by DNMT1, DNMT3A, and DNMT3B, with effects depending on genomic context [6]. Promoter methylation typically represses transcription, whereas gene body methylation may activate expression. Transcription factors (TFs) also shape methylation landscapes by recruiting or blocking DNMTs [7]. Recent studies demonstrate that lncRNAs can recruit DNMTs to regulate target gene expression, adding an additional layer of regulation [8]. MIR100HG has also been reported to modulate TGF-β signalling [9].  

## Project Goal  
This project aims to **predict the mode of action of MIR100HG** using patient data from five cancers (PAAD, LUAD, SKCM, PRAD, STAD) and their matched normal tissues. Specifically, we:  
1. Integrate **TF–target associations, DNA methylation, and gene expression** from TCGA cancer cohorts stratified by High/Low MIR100HG expression.  
2. Integrate **TF–target associations and gene expression** from GTEx normal tissues to investigate baseline MIR100HG regulation.  
3. Compare **cancer vs. normal tissues** to identify MIR100HG-driven features that are cancer-specific.  

## Methods Overview  
- **Expression subgrouping**: Samples stratified into High/Low MIR100HG using quantile thresholds (e.g. top/bottom 33%).  
- **Differential expression**: Welch’s t-test + Benjamini–Hochberg FDR correction across TFs and target genes.  
- **Methylation analysis**: Correlation of promoter CpG methylation with MIR100HG expression (Illumina 450K).  
- **TF prioritisation**: Combined statistical tests and Random Forest classification (feature importance scoring).  
- **Dimensionality reduction & network modelling**: PCA for subgroup visualisation; BFS traversal on ENCODE TF–target graphs to classify TFs as direct or indirect regulators.  

## Highlights  
- End-to-end reproducible pipeline: cohort harmonisation → subgrouping → DE/methylation → TF selection → PCA → network inference.  
- Multi-omics integration: TCGA RNA-seq, Illumina 450K methylation, ENCODE TF–target edges, GTEx normal expression.  
- Cancer–normal comparison: identifying **cancer-specific TF regulators** versus cross-cancer conserved signals.  
- Rich visualisation: volcano plots, correlation heatmaps, cross-tissue log2FC heatmaps, PCA scatterplots.  

## Data Sources  
- **Gene expression (cancers)**: TCGA RNA-seq TPM (log2(TPM+0.001)) [link](https://xenabrowser.net/datapages/?dataset=tcga_RSEM_gene_tpm&host=https%3A%2F%2Ftoil.xenahubs.net)  
- **TF–target associations**: ENCODE Transcription Factor–Targets (Harmonizome) [link](https://maayanlab.cloud/Harmonizome/dataset/ENCODE+Transcription+Factor+Targets)  
- **DNA methylation**: TCGA 450k methylation data for PAAD, LUAD, SKCM, PRAD, STAD (Illumina HumanMethylation450 BeadChip)  
- **Clinical data**: TCGA Pan-Cancer clinical tables (histological subtypes, metadata)  
- **Normal tissue expression**: GTEx RNA-seq TPM [link](https://xenabrowser.net/datapages/?dataset=gtex_rsem_isoform_tpm&host=https%3A%2F%2Ftoil.xenahubs.net)  
- **Normal tissue phenotypes**: GTEx phenotype tables  

## Data Access
Due to size limitations, raw datasets are hosted on OneDrive:  
[🔗 Download Data (OneDrive)](https://1drv.ms/f/s!AtSPOuyiZcMKcT0YIUPQxLhIZEE?e=p1TSUE)

## References
- Consortium, E. P. *et al.* (2007). *Identification and analysis of functional elements in 1% of the human genome by the ENCODE pilot project.* Nature.  
- Uszczynska-Ratajczak *et al.* (2018). *Towards a complete map of the human lncRNA transcriptome.* Nat. Rev. Genet.  
- Nemeth *et al.* (2024). *Non-coding RNAs in disease: from mechanisms to therapeutics.* Nat. Rev. Mol. Cell Biol.  
- Richardson *et al.* (2023). *Context-dependent TGF-β family signalling in cell fate regulation.* Nat. Rev. Mol. Cell Biol.  
- Ottaviani *et al.* (2018). *TGF-β induces miR-100 and miR-125b but blocks let-7a through LIN28B controlling PDAC progression.* Cell Death Dis.  
- Jin *et al.* (2012). *Linking DNA methyltransferases to epigenetic marks and nucleosome structure genome-wide in human tumour cells.* Cell Res.  
- Brenner *et al.* (2005). *Myc represses transcription through recruitment of DNA methyltransferase corepressor.* Nat. Genet.  
- Huang *et al.* (2022). *LncRNA-mediated DNA methylation: an emerging mechanism in cancer and beyond.* Cell Mol. Life Sci.  
- Papoutsoglou *et al.* (2021). *The noncoding MIR100HG RNA enhances autocrine function of transforming growth factor beta signalling.* Oncogene.  

---

> Repository maintained by [DearKarl](https://github.com/DearKarl). Contributions and feedback welcome.
