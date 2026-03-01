# MSc Applied Bioinformatics  

## Metagenomics Pipeline

Welcome to this repository, which provides an introductory guide to a metagenomics analysis pipeline.

This project includes step-by-step instructions for performing an initial analysis of metagenomic data, covering key stages from data acquisition to downstream processing. It is designed to help users build a solid understanding of both the concepts and practical workflows used in metagenomics.

---

#### Course Information
This material is part of an MSc course in Applied Bioinformatics, where the pipeline and code were taught and demonstrated by **Dr. Loukas Theodosiou**.

---

### What Does It Include?
- Downloading public metagenomic data  
- Preprocessing and quality control  
- Assembly and binning  
- Annotation of metagenome-assembled genomes (MAGs)  

---

### Getting Started
Follow the instructions in each section to run the pipeline step by step.

This pipeline covers the key steps in analyzing metagenomic data, from data download and preprocessing to the reconstruction and annotation of metagenome-assembled genomes. Additional steps are included to support further exploration and deeper analysis of the data.

## Download public data
SRA run selector
Download from terminal
#
`fastq-dump --split-files <accession_number>`
```bash
fastq-dump --split-files <accession_number>
