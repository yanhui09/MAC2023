---
layout: page
title: LACA
permalink: /exercieses/laca
parent: Exercises
nav_order: 2
---

1. TOC
{:toc}

---
## *De novo* OTU picking from long noisy amplicons with **LACA** 

[`LACA`](https://github.com/yanhui09/laca) is a reproducible and scalable workflow for Long Amplicon Consensus Analysis, e.g., 16S rRNA gene amplicon analysis. It uses `snakemake` to manage the workflow and `conda` to manage the environment.

## **LACA** installation

The full installation guide of `LACA` is available [here](https://github.com/yanhui09/laca#installation).

**`LACA` requires [`singularity`](https://en.wikipedia.org/wiki/Singularity_(software)) to use `guppy` in a visual container.**
**Since `singularity` is built for platform, `LACA` couldn't provide further support for `MacOS` users.**

**1.** Clone the Github repository and create an isolated `conda` environment
```
git clone https://github.com/yanhui09/laca.git
cd laca
mamba env create -n laca -f env.yaml 
```

**2.** Install `LACA` with `pip`
      
To avoid inconsistency, we suggest installing `LACA` in the above `conda` environment
```
conda activate laca
pip install --editable .
```

## A demo run with **LACA**

Find a full usage guide [here](https://github.com/yanhui09/laca#usage).

### Example with a quick start
```
conda activate laca                                  # activate required environment 
laca init -b /path/to/basecalled_fastqs -d /path/to/database    # init config file and check
laca run all                                         # start analysis
```

### Get familiar with `LACA` usage

`LACA` is easy to use. You can start a new analysis in two steps using `laca init` and `laca run` . 

Remember to activate the conda environment.
```
conda activate laca
laca -h
```

**1.** Intialize a config file with `laca init`

`laca init` will generate a config file in the working directory, which contains the necessary parameters to run `LACA`.

```
laca init -h
```

**2.** Start analysis with `laca run`

`laca run` will trigger the full workflow or a specfic module under defined resource accordingly.
Get a dry-run overview with `-n`. `Snakemake` arguments can be appened to `laca run` as well.

```
laca run -h
```

### Run `LACA` with a demo dataset

**0.** Make sure you have downlowded the required demo dataset from [here](https://github.com/yanhui09/MAC2023-extra). And the enter the directory with `cd`. 

E.g., Enter a directory with an absolute path ("long path") is `/home/me/MAC2023-extra`.
```
cd /home/me/MAC2023-extra
```

If you haven't downloaded the data yet and with `Git` installed,

```
git clone https://github.com/yanhui09/MAC2023-extra.git
cd ./MAC2023-extra 
```

**1.** Check where you are and try `laca init`, check the genereated `config.yaml` file.
```
pwd
laca init -b ./data/ont16s -d ./database -w ./laca_output --fqs-min 50
cat ./laca_output/config.yaml
```

**2.** Start `LACA` in a dry and real run
```
laca run all -w ./laca_output -n 
laca run isONclustCon -j 4 -m 20 -w ./laca_output      
```