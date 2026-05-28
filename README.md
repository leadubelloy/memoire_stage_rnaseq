# Comparative study of transcriptomic profiles (mRNA and miRNA) induced by exposure to conventional cigarettes and heated tobacco in mice

## Description
This repository contains the bioinformatic scripts used in the context of a Master 1 internship in Bioinformatics, OMICS and Systems Biology track, at the University of Lille — Faculty of Science and Technology, conducted within the IMPECS laboratory (ULR 4483), Research Center, Lille.

The study investigates transcriptomic dysregulations induced by exposure to **conventional cigarette smoke (1R6F)** and **heated tobacco (IQOS)** in mice (*Mus musculus*, A/J male strain), based on RNA-seq (mRNA) and small RNA-seq (miRNA) data from lung tissue.

- **Internship supervisor** : Dr. Sébastien Anthérieu
- **Academic tutor** : Dr. Morgane Baron
- **Year** : 2025-2026

---

## Analysis strategy

The bioinformatic analysis includes :
- **Filtering of dysregulated mRNAs and miRNAs** from DESeq2 pre-processed data provided by the IMPECS laboratory
- **Data visualization** (volcano plots, MA plots, heatmap, Venn diagrams)
- **Functional enrichment** GO:BP (ORA and GSEA) and KEGG (clusterProfiler)
- **miRNA/mRNA integration** using validated (multiMiR) and predicted (miRWalk) interactions
- **PPI network analysis** (STRING-db v12.0)

---

## Repository structure

### Scripts

| File | Description |
|------|-------------|
| `analyse_complete.Rmd` | Single R Markdown script containing the complete analysis: mRNA and miRNA filtering, visualization (volcano plots, MA plots, heatmap, Venn diagrams), functional enrichment GO/KEGG/GSEA, miRNA/mRNA integration (multiMiR, miRWalk) |

### Figures

| Folder | Content |
|--------|---------|
| `volcano_plots/` | Volcano plots for mRNA and miRNA |
| `MA_plots/` | MA plots for mRNA (cigarette and heated tobacco) |
| `venn_diagrams/` | Venn diagrams for mRNA and miRNA |
| `heatmap/` | Heatmap of the 41 common DEGs |
| `pie_charts/` | Pie charts for miRNA distribution (cigarette and heated tobacco) |
| `enrichissement/` | GO:BP ORA/GSEA dotplots and KEGG barplot |
| `reseaux_PPI/` | STRING-db networks (cigarette, heated tobacco, common) |

---

## Significance thresholds

| Data | Criterion | Fold Change |
|------|-----------|-------------|
| mRNA — cigarette | padj < 0.05 | \|log2FC\| ≥ 0.585 |
| mRNA — heated tobacco | padj < 0.05 | \|log2FC\| ≥ 0.585 |
| miRNA — cigarette | raw p-value < 0.05 | \|log2FC\| ≥ 0.585 |
| miRNA — heated tobacco | raw p-value < 0.05 | \|log2FC\| ≥ 0.585 |

> Raw p-value (< 0.05) was used for miRNAs in both conditions to allow consistent comparative analysis. For heated tobacco, no miRNA reached significance after multiple testing correction, while for cigarette, the relaxed threshold extends the panel beyond the 8 miRNAs significant after BH correction. All identified candidates require further experimental validation.

---

## miRNA/mRNA integration

Integration follows the canonical post-transcriptional repression logic :
- **miRNA UP × mRNA DOWN** : identification of repressed targets
- **miRNA DOWN × mRNA UP** : identification of derepressed targets

Two complementary levels of evidence :
1. **Validated interactions** — R package `multiMiR` v1.32.0 (miRTarBase, TarBase databases)
2. **Predicted interactions** — miRWalk v3 (filters: seed = 1, bindingp ≥ 0.95)

---

## Software and versions

| Tool | Version | Usage |
|------|---------|-------|
| R | 4.5.2 | Analysis environment |
| tidyverse (dplyr, tidyr) | 2.0.0 | Data manipulation |
| ggplot2 | 4.0.2 | Visualization |
| ggrepel | 0.9.6 | Volcano plot annotation |
| ggvenn | 0.1.19 | Venn diagrams |
| pheatmap | 1.0.13 | Common DEGs heatmap |
| clusterProfiler | 4.18.4 | Functional enrichment GO/KEGG/GSEA |
| org.Mm.eg.db | 3.22.0 | *Mus musculus* genomic annotation |
| multiMiR | 1.32.0 | Validated miRNA/mRNA integration |
| openxlsx | 4.2.8.1 | Interaction pairs export |
| STRING-db | v12.0 | PPI networks (web, *Mus musculus*) |
| miRWalk | v3 | Predicted miRNA/mRNA interactions |

---

## Key results

| Condition | Dysregulated mRNAs | Dysregulated miRNAs | Hub miRNA | Dominant biological profile |
|-----------|-------------------|---------------------|-----------|----------------------------|
| Conventional cigarette | 535 (410 UP / 125 DOWN) | 24 (15 UP / 9 DOWN) | mmu-miR-21a-5p (19 targets) | Genotoxicity, genomic instability, neutrophilic inflammation |
| Heated tobacco (IQOS) | 84 (28 UP / 56 DOWN) | 20 (14 UP / 6 DOWN) | mmu-miR-1a-3p (15 targets) | ECM remodeling, circadian disruption, immunosuppression |
| Common | 41 mRNAs (incl. *Lilrb4b* inversed) | 1 (mmu-miR-135b-5p, opposite regulation) | — | Circadian disruption, IL-17 inflammation |

> **Common miRNA-regulated core** : *Dio2*, *Ikzf4*, *Nfil3*, *Npas2*, *S100a8*, *Spaar*

---

## Author

**DUBELLOY Léa** — Master 1 Bioinformatics, OMICS and Systems Biology track  
University of Lille — Faculty of Science and Technology  
IMPECS Laboratory (ULR 4483), Research Center, Lille — 2025-2026
