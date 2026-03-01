# MSc Applied Bioinformatics  

# Introduction to Metagenomics 

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

# Metagenomics Pipeline

## 1. Download Public Data

### 1.1 <u>SRA Run Selector</u>

The Sequence Read Archive (SRA) Run Selector is a web-based tool that allows you to search and download metagenomics datasets.

You can access it here:  
→ https://www.ncbi.nlm.nih.gov/Traces/study/

For this course, you will use the dataset with accession number:

**PRJNA448333**

From the following publication:  
→ https://microbiomejournal.biomedcentral.com/articles/10.1186/s40168-019-0618-5#Sec2

Use the search functionality to locate the dataset and note the accession numbers of the samples you want to download.


### 1.2 Download from the Terminal

Once you have the accession numbers, you can use the **SRA Toolkit** to download the data from the command line.

First, make sure the toolkit is installed on your system.

Then run:

```bash
fastq-dump --split-files <accession_number>
```

## 2. Data preprocessing
### 2.1 Quality control (QC)

To perform Quality Control you have to use tools like:
- Multi QC
- FastQC
  
These tools will give you metrics such as: read quality scores, GC content, and sequence duplication levels,
which will help you to identify any potential issues with the data.

```
mkdir fastqc_out

# Example command to run FastQC
for each in *.fastq.gz
do 
fastqc ${each} -o fastqc
```

### 2.2 Trimmomatic

The next step is to trim adapter sequences, if present, and remove the low-quality reads from the data.

```
# Example command to run Trimmomatic
trimmomatic PE -threads 4 -phred33 input_forward.fastq.gz input_reverse.fastq.gz \
                output_forward_paired.fastq.gz output_forward_unpaired.fastq.gz \
                output_reverse_paired.fastq.gz output_reverse_unpaired.fastq.gz \
                ILLUMINACLIP:TruSeq3-PE.fa:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36
```
## 3. Assembly of the data into contigs
Use the metaSPAdes tool to assemble the preprocessed reads into contigs.

```
# Example command to run metaSPAdes
metaspades.py -1 input_forward_paired.fastq.gz -2 input_reverse_paired.fastq.gz -o metaspades_output

```
## 4. Generate coverage statistics

To generate coverage statistics by mapping reads to the contigs we need to use:

- bwa
→ http://bio-bwa.sourceforge.net/
- samtools software
→ http://www.htslib.org/ ,

 right before running MetaBAT, to reformat the output.

 ```
# index the contigs file that was produced by metaSPAdes:
bwa index contigs.fasta

# map the original reads to the contigs:
bwa mem contigs.fasta input_forward_paired.fastq input_reverse_paired.fastq > input.fastq.sam

# reformat the file with samtools:
samtools view -Sbu input.fastq.sam > junk
samtools sort junk input.fastq.sam
```

## 5. Create metagenome-assembled genomes (MAGs)

To bin the assembled contigs into putative metagenome-assembled genomes (MAGs), we use MetaBAT2:

```
# Example command to run MetaBAT2
metabat2 -i metaspades_output/contigs.fasta -o metabat2_output/bin \
         -m 1500 --unbinned \
         --saveCls metabat2_output/bin.cls.tsv \
         --saveLog metabat2_output/metabat2.log
```
Then use CheckM and BUSCO or EukCC to estimate the completeness and quality of the resulting MAGs:

```
# Example command to run CheckM
checkm lineage_wf -t 4 -x fa metabat2_output/bin checkm_output

```

## 6. Visualising the phylogenetic tree

To plot and visualize the tree we have produced we can use a free, web-based tool → iTOL (interactive Tree of Life): http://itol.embl.de/index.shtml
iTOL only takes in newick formatted trees, so we need to quickly reformat the tree with FigTree (http://tree.bio.ed.ac.uk/software/figtree/).

## 7. Annotation

The last step is to annotate the MAGs. To do that we use tools like: 

- Prokka
- eggNOG-mapper

```
# Example command to run Prokka
prokka --outdir prokka_output --prefix sample_name metaspades_output/contigs.fasta

```
---

# Conclusion

This pipeline provides a complete workflow for an introductory metagenomics analysis.  
Starting from public raw sequencing data, it guides the user through:

- Data download and preprocessing  
- Quality control and trimming  
- Assembly of reads into contigs  
- Generation of coverage statistics  
- Binning contigs into metagenome-assembled genomes (MAGs)  
- Evaluation of MAG completeness and quality  
- Phylogenetic visualization and genome annotation  

Following these steps will help users understand the key concepts and practical methods used in metagenomics, and provide a foundation for more advanced analyses in microbial ecology and evolutionary studies.
