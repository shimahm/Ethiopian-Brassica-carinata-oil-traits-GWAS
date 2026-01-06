# Ethiopian-Brassica-carinata-oil-traits-GWAS

“A reproducible companion repository for the Ethiopian B. carinata oil composition/seed colour GWAS manuscript: data processing, GWAS post-processing, genome functional annotation, haplotype effects, GO enrichment, and key figures.”

This repository contains the reproducible analysis workflow for the manuscript:

**[Genetic architecture of fatty acid composition, oil content, and seed color in a diverse collection of Ethiopian Brassica carinata]**  
Shima Mahmoudi et al.

It documents all major analysis steps:
- phenotype QC + summary statistics
- GWAS post-processing and locus definition
- Arabidopsis-based functional enrichment of the *B. carinata* genome annotation (RBH + GO transfer)
- candidate gene mapping around loci
- haplotype (LD-block) effect testing and visualization
- GO enrichment analysis for locus candidate genes
- generation of manuscript figures and tables

> Note: raw sequencing data and restricted-access phenotype files are not redistributed here. This repository provides scripts, metadata, and a reproducible structure for rerunning analyses on authorised systems (HPC/local).

---

## 1) Repository structure

This repository is organised to be a lightweight umbrella that points to the code and versions used for the manuscript. It does not duplicate large datasets or every pipeline — instead it pins commits, records run order, and stores final figure-generation scripts and metadata.

.
├── 00_project_overview/  
│   ├── manuscript_links.md  
│   ├── data_dictionary.md  
│   └── analysis_plan.md  
├── 01_inputs/  
│   ├── phenotype/           # cleaned phenotype tables used in GWAS  
│   ├── metadata/            # accession / seed colour / altitude metadata  
│   └── reference/           # pointers (paths) to reference genome + GFF3  
├── 02_genome_annotation/  
│   └── README.md            # how to reproduce Arabidopsis-transfer annotation  
├── 03_gwas_postprocessing/  
│   ├── configs/  
│   ├── scripts/  
│   └── outputs/  
├── 04_haplotype_effects/  
│   ├── block_definitions/  
│   ├── scripts/  
│   └── outputs/  
├── 05_go_enrichment/  
│   ├── scripts/  
│   └── outputs/  
├── 06_figures_tables/  
│   ├── figure_scripts/      # scripts used to build final manuscript figures  
│   ├── table_scripts/       # scripts used to build manuscript tables  
│   └── outputs/             # final figure + table files (png/pdf/csv)  
├── envs/  
│   ├── conda_env.yml  
│   └── sessionInfo_R.txt  
└── CITATION.cff

---

## 2) External pipeline modules (authored by S. Mahmoudi)

This project reuses the following repositories. In workflow documentation we pin to specific commits/tags for reproducibility.

- Genome annotation with Arabidopsis ortholog/GO transfer:  
  https://github.com/shimahm/-Brassica-carinata-Genome-Annotation-Pipeline

- Post-GWAS SNP annotation (significant SNPs → genes overlap/nearby):  
  https://github.com/shimahm/post_gwas_SNP_annotation

- GWAS → GO enrichment one-command pipeline:  
  https://github.com/shimahm/GWAS-GO-Enrichment-Pipeline

- LD-block haplotype effects + dominant-haplotype violin plots:  
  https://github.com/shimahm/Reproducible-Haplotype-Effect-Pipeline

---

## 3) Reproducibility

### Software
- R (>= 4.1) + packages listed in `envs/`
- Python 3 (pandas, numpy, etc.)
- PLINK, bcftools, bedtools
- DIAMOND (for RBH orthology)
- Standard UNIX utilities (awk, sed, grep)

### Environments
A minimal conda environment is provided at `envs/conda_env.yml`. Create and activate with:

```bash
conda env create -f envs/conda_env.yml
conda activate bcarinata_oil_gwas
```

Record the R session used for figure/table generation in `envs/sessionInfo_R.txt` (provided).

---

## 4) Recommended run order (high level)

1. Genome annotation enrichment (Arabidopsis RBH + transfer GO terms into GFF3)  
2. GWAS post-processing (filter significant SNPs, define loci/haploblocks, map nearby genes)  
3. Haplotype effect analysis (LD blocks, PCs, dominant-haplotype violin plots)  
4. GO enrichment (candidate gene sets per locus)  
5. Figures & tables (final plots, summary tables for manuscript)

The `00_project_overview/analysis_plan.md` contains exact commands, pinned commit SHAs for each external pipeline, and which script produces which figure/table.

---

## 5) Inputs & data availability

- Raw reads: [SRA/ENA accession or “available upon request”]  
- Reference genome & annotation: 

---

## 6) Citation

If you use this repository, please cite the associated manuscript.

