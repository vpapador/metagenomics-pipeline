# MSc Applied Bioinformatics 
## Metagenomics-72556
This repository provides an introductory guide to a metagenomics analysis pipeline. It includes step-by-step instructions for performing an initial analysis of metagenomic data, covering essential stages from data acquisition to downstream processing. The material is designed to help users become familiar with core concepts and practical workflows in metagenomics. The course and accompanying code were taught and demonstrated by Dr. Loukas Theodosiou.

# 🧬 Metagenomics Pipeline

Welcome to this repository, which provides an introductory guide to a metagenomics analysis pipeline.  

This project includes step-by-step instructions for performing an initial analysis of metagenomic data, covering key stages from data acquisition to downstream processing. It is designed to help users build a solid understanding of both the concepts and practical workflows used in metagenomics.

---

## 📚 Course Information
This material is part of a course where the pipeline and code were taught and demonstrated by **Dr. Loukas Theodosiou**.

---

## 🚀 What You'll Learn
- Downloading public metagenomic data  
- Preprocessing and quality control  
- Assembly and binning  
- Annotation of metagenome-assembled genomes (MAGs)  

---

## 🛠️ Getting Started
Follow the instructions in each section to run the pipeline step by step.

This pipeline covers the key steps in analyzing metagenomics data, from data download and preprocessing to the creation of metagenome-assembled genomes and their annotation. The extra steps provide opportunities for further exploration and analysis of the data.
## Download public data
SRA run selector
Download from terminal
#
`fastq-dump --split-files <accession_number>`
```bash
fastq-dump --split-files <accession_number>
