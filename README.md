# Comparative study of transcriptomic profiles (mRNA and miRNA) induced by exposure to conventional cigarettes and heated tobacco in mice

## Description
Ce dépôt contient les scripts bio-informatiques utilisés dans le cadre du mémoire de stage de Master 1 Bio-informatique, parcours OMICS and Systems Biology, à l'Université de Lille — Faculté des Sciences et Technologies, réalisé au sein du laboratoire IMPECS (ULR 4483), Pôle Recherche, Lille.

L'étude porte sur les dérégulations transcriptomiques induites par l'exposition à la **fumée de cigarette conventionnelle (1R6F)** et au **tabac chauffé (IQOS)** chez la souris (*Mus musculus*, souche A/J mâle), à partir de données RNA-seq (ARNm) et small RNA-seq (miARN) issues de tissu pulmonaire.

- **Maître de stage** : Dr. Sébastien Anthérieu
- **Tutrice académique** : Dr. Morgane Baron
- **Année** : 2025-2026

---

## Stratégie d'analyse

L'analyse bio-informatique comprend :
- Un **filtrage des ARNm et miARN dérégulés** à partir de données DESeq2 pré-calculées fournies par le laboratoire IMPECS
- Une **visualisation** des données (volcano plots, MA plots, heatmap, diagrammes de Venn)
- Un **enrichissement fonctionnel** GO:BP (ORA et GSEA) et KEGG (clusterProfiler)
- Une **intégration miARN/ARNm** par interactions validées (multiMiR) et prédites (miRWalk)
- Une **analyse de réseaux PPI** (STRING-db v12.0)

---

## Contenu du dépôt

### Scripts

| Fichier | Description |
|---------|-------------|
| `analyse_complete.Rmd` | Script R Markdown unique contenant l'ensemble de l'analyse : filtrage des ARNm et miARN, visualisation (volcano plots, MA plots, heatmap, Venn), enrichissement fonctionnel GO/KEGG/GSEA, intégration miARN/ARNm (multiMiR, miRWalk) |

### Figures

| Dossier | Contenu |
|---------|---------|
| `volcano_plots/` | Volcano plots ARNm et miARN |
| `MA_plots/` | MA plots ARNm (cigarette et tabac chauffé) |
| `venn_diagrams/` | Diagrammes de Venn ARNm et miARN |
| `heatmap/` | Heatmap des 41 DEGs communs |
| `enrichissement/` | Dotplots GO:BP ORA/GSEA et barplot KEGG |
| `reseaux_PPI/` | Réseaux STRING-db (cigarette, tabac chauffé, commun) |
---

## Seuils de significativité

| Données | Critère | Fold Change |
|---------|---------|-------------|
| ARNm — cigarette | padj < 0,05 | \|log2FC\| ≥ 0,585 |
| ARNm — tabac chauffé | padj < 0,05 | \|log2FC\| ≥ 0,585 |
| miARN — cigarette | p-value brute < 0,05 | \|log2FC\| ≥ 0,585 |
| miARN — tabac chauffé | p-value brute < 0,05 | \|log2FC\| ≥ 0,585 |

> La p-value brute (< 0,05) est utilisée pour les miARN des deux conditions afin de permettre une analyse comparative cohérente. Pour le tabac chauffé, aucun
> miARN n'atteignait le seuil strict, tandis que pour la cigarette, le recours à la p-value brute permet d'élargir le panel au-delà des 8 miARN significatifs
> après correction multiple. Les candidats identifiés nécessitent une validation expérimentale ultérieure.

---

## Intégration miARN/ARNm

L'intégration suit la logique canonique de répression post-transcriptionnelle :
- **miARN UP × ARNm DOWN** : identification des cibles réprimées
- **miARN DOWN × ARNm UP** : identification des cibles déréprimées

Deux niveaux de preuve complémentaires :
1. **Interactions validées** — package R `multiMiR` v1.32.0 (bases miRTarBase, TarBase)
2. **Interactions prédites** — miRWalk v3 (seed = 1, bindingp ≥ 0,95)

---

## Logiciels et versions

| Outil | Version | Usage |
|-------|---------|-------|
| R | 4.5.2 | Environnement d'analyse |
| tidyverse (dplyr, tidyr) | 2.0.0 | Manipulation des données |
| ggplot2 | 4.0.2 | Visualisation |
| ggrepel | 0.9.6 | Annotation des volcano plots |
| ggvenn | 0.1.19 | Diagrammes de Venn |
| pheatmap | 1.0.13 | Heatmap des DEGs communs |
| clusterProfiler | 4.18.4 | Enrichissement fonctionnel GO/KEGG/GSEA |
| org.Mm.eg.db | 3.22.0 | Annotation génomique *Mus musculus* |
| multiMiR | 1.32.0 | Intégration miARN/ARNm validée |
| openxlsx | 4.2.8.1 | Export des paires d'interaction |
| STRING-db | v12.0 | Réseaux PPI (web, *Mus musculus*) |
| miRWalk | v3 | Interactions prédites miARN/ARNm |

---

## Principaux résultats

| Condition | ARNm dérégulés | miARN dérégulés | Hub miARN | Profil biologique dominant |
|-----------|----------------|-----------------|-----------|----------------------------|
| Cigarette conventionnelle | 535 (410 UP / 125 DOWN) | 24 (15 UP / 9 DOWN) | mmu-miR-21a-5p (19 cibles) | Génotoxicité, instabilité génomique, inflammation neutrophilique |
| Tabac chauffé (IQOS) | 84 (28 UP / 56 DOWN) | 20 (14 UP / 6 DOWN) | mmu-miR-1a-3p (15 cibles) | Remodelage ECM, perturbation circadienne, immunosuppression |
| Commun | 41 ARNm (dont *Lilrb4b* inversé) | 1 (mmu-miR-135b-5p, sens inversé) | — | Perturbation circadienne, inflammation IL-17 |

> **Core miARN-régulé commun** : *Dio2*, *Ikzf4*, *Nfil3*, *Npas2*, *S100a8*, *Spaar*

---

## Auteure

**DUBELLOY Léa** — Master 1 Bio-informatique, parcours OMICS and Systems Biology  
Université de Lille — Faculté des Sciences et Technologies  
Laboratoire IMPECS (ULR 4483), Pôle Recherche, Lille — Année 2025-2026
