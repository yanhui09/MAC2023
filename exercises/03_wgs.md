---
layout: page
title: WGS
permalink: /exercieses/wgs
parent: Exercises
has_toc: true
nav_order: 4
---

1. TOC
{:toc}

---
## Genome assembly with 2nd and 3rd WGS data

In this session, we aim to assemble a bacterial genome using 2nd and 3rd whole genome sequencing (WGS) data. 
We will use it this as example to explore the WGS data analysis, and look into the difference between sequencing technologies.

## Software installation with `mamba`

It's recommended to install the software with `mamba` in a **independent** conda environment.

Assuming you have installed `mamba` in your system, you can create a new conda environment with `mamba` and install the software with the following commands:

Go to the downloaded data directory. *Make sure you know where you are in the terminal.*

E.g., The downloaded data directory is placed at /home/username/MAC2023-extera.

```
cd /home/username/MAC2023-extera
pwd
```

You shall see the path of the downloaded data directory as below.
```
/home/username/MAC2023-extera
```

Now you can create a new conda environment with `mamba` and install the software with the following commands:

```
mamba env create -n wgs1 -f envs/env1.yaml
```

Activate the environment for the following analysis.

```
conda activate wgs1
```

## Exporation with a demo data

The WGS data can be fetched from [MAC2023-extra](https://github.com/yanhui09/MAC2023-extra) as before.
You shall download the data already if you have completed the previous exercises. In case you haven't, you can refer to the [requisites](https://yanhui09.github.io/MAC2023/exercieses/requisites) section.   

### First look at the data with `seqkit` and `fastqc`

```
seqkit stat data/wgs/*.fastq.gz data/wgs/ncbi_pacbio_TL110.fasta
```

Expected output:
```
file                              format  type  num_seqs     sum_len    min_len    avg_len    max_len
data/wgs/NXT20x_R1.fastq.gz       FASTQ   DNA    200,000  30,200,000        151        151        151
data/wgs/NXT20x_R2.fastq.gz       FASTQ   DNA    200,000  30,200,000        151        151        151
data/wgs/ont_r10_20x.fastq.gz     FASTQ   DNA      7,862  51,201,670        129    6,512.6     87,688
data/wgs/ncbi_pacbio_TL110.fasta  FASTA   DNA          1   2,566,312  2,566,312  2,566,312  2,566,312
```

Here is a set of sequencing data from a *Propionibacterium freudenreichii* strain. 
We subsampled the sequencing data to 20x coverage for the Illumina and Nanopore reads. 
The PacBio reference genome is from the [NCBI RefSeq database](https://www.ncbi.nlm.nih.gov/nuccore/NZ_CP085641.1). 

{: .note-question}
*Q1: What is the genome size of this strain? How is the sequencing coverage calculated?*
illumina: 30,200,000*2/2,566,312≈20
ONT: 51,201,670/2,566,312≈20

Let's have a look at the quality of the sequencing data with `fastqc`.

```
mkdir -p fastqc/illumina fastqc/ont_r10
fastqc data/wgs/NXT20x_R*.fastq.gz -o ./fastqc/illumina
fastqc data/wgs/ont_r10_20x.fastq.gz -o ./fastqc/ont_r10
```

You can open the html files in the `fastqc` directory to have a look at the quality of the sequencing data.

**Illumina**
![Illumina](./assessts/03_wgs/read_illumina.png)

**Nanopore**
![Nanopore](./assessts/03_wgs/read_ont.png)

{: .note-note}
We could see the ONT reads is way longer but contains more errors than the Illumina reads. 

### Genome assembly with Illumina reads

#### Adapter removal with `trimmomatic`

`trimmomatic` is a tool for trimming adapters and low quality reads. It is a java program.
```

#### Reads quality control with `bbmap`

#### Genome assembly with `spades`  

### Genome assembly with Nanopore reads

#### Optional: Adapter removal with `guppy` or `porechop`

#### Reads quality control with `seqkit`

#### Genome assembly with `flye`

#### Genome polishing with `racon` and `medaka`

### Hybrid assembly with Nanopore and Illumina reads

#### Illumina reads polishing with `pilon`

#### Optional: hybrid assembly with `unicycler`

### Quality assessment of assembled genomes with `quast`

### Optional: Reference-guided correction with `proovframe`

#### Genome annotation with `prokka`

#### Frameshift correction with `proovframe`



