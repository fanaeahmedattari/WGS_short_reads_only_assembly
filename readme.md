# Short‑Read Assembly of *Bacteroides fragilis* S01

<div align="center">

# 🔬 Short‑Read Assembly: A Learning Journey

[![Conda](https://img.shields.io/badge/Environment-Conda-lightgrey)](#)
[![Bioinformatics](https://img.shields.io/badge/Domain-Bioinformatics-blue.svg)]()
[![Project](https://img.shields.io/badge/Type-Short%20Read%20Assembly-orange.svg)]()

*A clear, easy‑to‑follow set of tools for assembling genomes from short reads, designed for reliable and transparent results.*

</div>

## Overview
This repository provides a reproducible, end‑to‑end pipeline for assembling the genome of a multidrug‑resistant *Bacteroides fragilis* clinical isolate (strain S01, accession **DCMSKEJBY0001B**). The workflow is written in Bash, uses Conda for dependency management, and follows current best practices for whole‑genome short‑read analysis.

## Data Summary
- **Organism:** *Bacteroides fragilis* (clinical isolate)
- **Strain:** S01 (DCMSKEJBY0001B)
- **Sequencing platform:** Illumina MiSeq, 150 bp paired‑end
- **Raw data:** Available via NCBI SRA (SRR8893090, BioProject PRJNA244942). FASTQ files are not stored in the repository; a `metadata.csv` file describes their locations.

## Repository Structure
```
short_reads_only_assembly/
├── 00_raw_reads/               # metadata.csv describing raw FASTQ files (FASTQs excluded)
├── analysis.sh                 # master driver script orchestrating the workflow
├── installation.sh              # Conda/Mamba environment setup script
├── readme.md                    # this documentation
└── (large intermediate directories such as 01_qc_before_processing, 02_process_reads, etc. are omitted to keep the repo lightweight)
```

## Installation & Setup
```bash
# Clone the repository
git clone https://github.com/fanaeahmedattari/short_reads_only_assembly.git
cd short_reads_only_assembly

# Create the Conda environment and install dependencies
bash installation.sh
```
The `installation.sh` script creates a dedicated Conda environment, installs tools (FastQC, Trimmomatic, SPAdes, QUAST, Prokka, etc.), and verifies versions.

## Running the Workflow
1. Populate `00_raw_reads/metadata.csv` with the paths to your paired‑end FASTQ files (or download them directly from SRA).
2. Launch the pipeline:
```bash
bash analysis.sh
```
The script sequentially performs:
- **Quality control** (FastQC, MultiQC) before and after trimming
- **Read preprocessing** (Trimmomatic) to remove adapters and low‑quality bases
- **De novo assembly** using SPAdes in careful mode
- **Assembly assessment** (QUAST, BUSCO) to evaluate contiguity and completeness
- **Functional annotation** (Prokka) to predict genes and assign product names

All intermediate and final outputs are organized in dedicated sub‑directories for easy inspection.

## Results Highlights (example)
- Assembled genome size: ~5.5 Mb
- N50: 112 kb
- BUSCO completeness: 96 % (single‑copy bacterial genes)
- Annotation: ~4 800 protein‑coding genes identified by Prokka
*(Replace with your actual results.)*

## Reproducibility & Best Practices
- All software versions are pinned in the Conda environment file (`environment.yml`).
- The pipeline is fully scripted; no manual intervention is required after providing FASTQ paths.
- Output logs are captured for each step, enabling traceability and debugging.
- The repository follows FAIR principles: Findable, Accessible, Interoperable, Reusable.

## Acknowledgment
Special thanks to Dr. Muhammad Aammar Tufail and the Codanics platform. The projects in this repository were developed and refined as part of the **"Bioinformatics ka Chilla"** course, which provided the foundational knowledge and technical training required to master WGS analysis.

---
<small>
## **Author:** Fana e Ahmed Attari<br>
## **GitHub:** fanaeahmedattari
<small>
---
