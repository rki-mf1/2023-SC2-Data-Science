1. Clone repository
```
git clone https://github.com/KleistLab/GInPipe/tree/main
```
2. Install (mini)conda 
Conda will manage the dependencies of our pipeline. Instructions can be found here: https://docs.conda.io/projects/conda/en/latest/user-guide/install.

3. Create working environment
3.1. Create and ativate environment from environment file and install Snakemake
```
conda env create -f env/env.yml
conda activate GInPipe
conda install -c conda-forge -c bioconda snakemake
```
3.2. If an error occurs, try to install packages via mamba
From **base**:
```
conda install -c conda-forge mamba
```
Add channels where mamba/conda will look for the pakages:
```
conda config --add channels r 
conda config --add channels agbiome
conda config --add channels conda-forge
conda config --add channels bioconda 
conda config --add channels anaconda   
```
Make an environment using mamba 
```
mamba create -y -p env/tutorial bbmap pip seqkit samtools numpy==1.20.0 pysam biopython pandas scipy minimap2 pyvcf
conda activate env/tutorial
pip install git+https://github.com/KleistLab/ginpipepy
mamba install -c conda-forge -c bioconda snakemake
```
3.3. It may be that if you have a newer Mac with M1/M2 chip some packages will not install via conda (the prompt will say that some packages were not found). In this case:
From **base**:
```
conda install -c conda-forge mamba
```
Add channels where mamba/conda will look for the pakages:
```
conda config --add channels r 
conda config --add channels agbiome
conda config --add channels conda-forge
conda config --add channels bioconda 
conda config --add channels anaconda   
```
Make an environment using mamba skipping packages mamba couldn't install, in our case:
```
mamba create -y -p env/tutorial bbmap pip numpy==1.20.0 biopython pandas scipy 
```
Activate the new environment:
```
conda activate env/tutorial
```
Install packages with pip:
```
pip install PyVCF
pip install pysam
pip install git+https://github.com/KleistLab/ginpipepy
```
Install packages with brew (how to install brew: https://brew.sh)
```
brew install samtools
brew install seqkit
brew install minimap2
```
And install Snakemake:
```
mamba install -c conda-forge -c bioconda snakemake
```
4. Install R routines
```
conda install -c conda-forge -c bioconda r-base r-ggplot2 r-r0 r-scales r-devtools
```
5. Conflicts with PyVCF and setuptools: removed import of masking function from ginpipepy!!!!