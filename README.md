# MSc Applied Bioinformatics  

# Metagenomics Pipeline

Welcome to this repository, which provides an introductory guide to a metagenomics analysis pipeline.

This project includes step-by-step instructions for performing an initial analysis of metagenomic data, covering key stages from data acquisition to downstream processing. It is designed to help users build a solid understanding of both the concepts and practical workflows used in metagenomics.


#### Course Information
This material is part of an MSc course in Applied Bioinformatics, where the pipeline and code were taught and demonstrated by **Dr. Loukas Theodosiou**.


#### What Does It Include?
- Downloading public metagenomic data  
- Preprocessing and quality control  
- Assembly and binning  
- Annotation of metagenome-assembled genomes (MAGs)  


#### Getting Started
Follow the instructions in each section to run the pipeline step by step.

This pipeline covers the key steps in analyzing metagenomic data, from data download and preprocessing to the reconstruction and annotation of metagenome-assembled genomes. Additional steps are included to support further exploration and deeper analysis of the data.

---

## 1. Download Public Data

### 1.1 <u>SRA Run Selector</u>

The Sequence Read Archive (SRA) Run Selector is a web-based tool that allows you to search and download metagenomics datasets.

You can access it here:  
👉 https://www.ncbi.nlm.nih.gov/Traces/study/

For this course, you will use the dataset with accession number:

**PRJNA448333**

From the following publication:  
👉 https://microbiomejournal.biomedcentral.com/articles/10.1186/s40168-019-0618-5#Sec2

Use the search functionality to locate the dataset and note the accession numbers of the samples you want to download.


### 1.2 Download from the Terminal

Once you have the accession numbers, you can use the **SRA Toolkit** to download the data from the command line.

First, make sure the toolkit is installed on your system.

Then run:

```bash
fastq-dump --split-files <accession_number>
