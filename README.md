# Hi-GLMM (HiGLMM)

## 1.Getting started

### 1.1	Downloading HiGLMM

Hi-GLMM can be downloaded from https://github.com/RunKingProgram/Hi-GLMM. It can be installed as a regular R package.

### 1.2	Installing HiGLMM

**HiGLMM** links to R packages Rcpp, RcppEigen, RcppArmadillo,BEDMatrix and data.table. These dependencies should be installed before installing HiGLMM. In addition, HiGLMM **requires PLINK2.0 Software (http://www.cog-genomics.org/plink/2.0/) with name “plink2” under your working directory**. Here is an example for installing HiGLMM and all its dependencies in an R session(assuming none of the R packages other than the default has been installed):
```
install.packages(c( "Rcpp", "RcppArmadillo", "RcppEigen", "BEDMatrix", "data.table", "parallel", "snow"), repos = "https://cran.r-project.org/")
system(“R CMD install HiGLMM_1.0.tgz”)
```

## 2. Input

HiGLMM requires the phenotype and genotype files in an **PLINK BED** format which also called PLINK 1 binary file and the structure of these files is described in http://www.cog-genomics.org/plink/1.9/formats#bed. Preparation of these data are described below.

### 2.1 Phenotype

Phenotype should place in the sixth column of “.fam” file. 

### 2.2 Genotypes

GRL can only take genotype files in PLINK “.bed” and “.bim” format.

## 3. Running HiGLMM
If **HiGLMM** has been successfully installed, you can load it in an R session using:<br>
```
library(HiGLMM)
```
and then loading "BEDMatrix ", " data.table ", "parallel", "snow" <br>
```
library(BEDMatrix)
library(data.table)
library(parallel)
library(snow)
```
We provide three functions in **HiGLMM**: **Data_HiGLMM** function for basic data management including extracting phenotypic values, sampling markers, calculating allele frequencies and GRM (saved in external files) and **HiGLMM** function for estimating heritability (optional) and breeding values, implementing association tests using HiGLMM method .


