# Hands-on session Day 4: Incidence estimation

## Introduction
In this hands-on session we will be working with a pipeline tool called [GInPipe](https://github.com/KleistLab/GInPipe) implemented in Snakemake. This pipeline infers the trajectory of an effective population size (or incidence) for a viral pandemic from a collection of time-stamped viral sequences. The pipeline has so far been tested for SARS-CoV-2.
In brief: Viral sequence data is placed into redundant temporal bins. For each bin, a parameter is inferred that correlates with the effective population size estimate (or incidence) of the infection. GInPipe then smoothes over all derived parameters and reconstructs continuous trajectory of the effective population size estimate (or incidence) [[1]](#1).

The pipeline uses the following dependencies:

```
- python=3.9.18
- snakemake=7.32.3
- biopython=1.78
- pandas=2.0.3
- scipy=1.11.1
- bbmap=38.18
- numpy=1.24.4
- matplotlib=3.7.2
- scikit-fda=0.8.1
- pysam=0.21.0
- seqkit=2.4.0
- samtools=1.17
- minimap2=2.26
```

## Installation
### 1. Clone repository
```
git clone https://github.com/KleistLab/GInPipe
```
Or download the latest release: https://github.com/KleistLab/GInPipe/releases/tag/v3.0.0

### 2. Install (mini)conda 
Conda will manage the dependencies of our pipeline. Installation instructions can be found here: https://docs.conda.io/projects/conda/en/latest/user-guide/install.

### 3. Create working environment

Switch to whatever directory you put the GInPipe repository into:
```
cd path/to/ginpipe
```

#### 3.1. Create and activate environment
```
conda env create -f env/env.yml
conda activate GInPipe3
```
#### 3.2. If an error occurs, try to install packages via mamba
Follow the instructions to install Mamba: https://mamba.readthedocs.io/en/latest/mamba-installation.html

Add channels where mamba/conda will look for the packages:
```
conda config --add channels r 
conda config --add channels agbiome
conda config --add channels conda-forge
conda config --add channels bioconda 
conda config --add channels anaconda   
```
Make an environment using mamba. Give it a different name to not cause conflicts with provided environment in *env/env.yml*, e.g. *tutorial*:
```
mamba create -y -p env/tutorial bbmap pip seqkit samtools numpy pysam biopython pandas scipy minimap2 pyvcf
```
Activate the new environment:
```
conda activate env/tutorial
```
### 4. Installation on M1/M2 Mac
 If you have a newer Mac with M1/M2 chip some packages might not install via conda/mamba. If this is the case, follow instructions below.

Follow the instructions to install Mamba: https://mamba.readthedocs.io/en/latest/mamba-installation.html

Add channels where mamba/conda will look for the packages:
```
conda config --add channels r 
conda config --add channels agbiome
conda config --add channels conda-forge
conda config --add channels bioconda 
conda config --add channels anaconda   
```
Make a new environment using mamba skipping packages that mamba couldn't install (in this case **pysam**,**samtools**, **seqkit** and **minimap2**). Give it a different name to not cause conflicts with provided environment in *env/env.yml*, e.g. *tutorial*:
```
mamba create -y -p env/tutorial bbmap pip numpy biopython matplotlib pandas scipy scikit-fda
```
Activate the new environment:
```
conda activate env/tutorial
```
Install packages with pip:
```
pip install pysam
```
Install packages with brew (https://brew.sh)
```
brew install samtools
brew install seqkit
brew install minimap2
```

[Next: initialize and run GInPipe](hands-on_2_run.md)


## Reference
<a id="1">[1]</a>
Smith, M. R. and Trofimova, M., et al. (2021). Rapid incidence estimation from SARS-CoV-2 genomes reveals decreased case detection in Europe during summer 2020. Nature Communications  12, 6009. https://doi.org/10.1038/s41467-021-26267-y
