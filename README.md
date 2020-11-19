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
and then loading "BEDMatrix ", " data.table ", "parallel" and "snow". <br>
```
library(BEDMatrix)
library(data.table)
library(parallel)
library(snow)
```
We provide three functions in **HiGLMM**: **Data_HiGLMM** function for basic data management including extracting phenotypic values, sampling markers, calculating allele frequencies and GRM (saved in external files) and **HiGLMM** function for estimating heritability (optional) and breeding values, implementing association tests using HiGLMM method .


### 3.1 Data_HiGLMM function
#### Usage
```
Data_HiGLMM(filename,h2,ebv)
```
#### Arguments
#### filename
An object class of character: the filename of PLINK BED files. The three PLINK files must have the same filename, for example, “filename.bed”, “filename.bim” and “filename.bam”.<br>
#### h2
An optional numeric for the number of heritability. If this is unset, estimate heritability.<br>
#### ebv
An optional matrix for estimating breeding values. If this is unset, estimate breeding values.<br>

### 3.2 HiGLMM function
#### Usage
```
HiGLMM (Data, Test ,thread,QQ,Manh)
```
#### Arguments

#### Data
An object class of list generated from the **Data_HiGLMM** function.
#### Test
An optional for association test, a test at once or the joint analysis. You can choose “Separate” for a test at once and “Joint” for further joint analysis based on the result of “Separate”.
#### thread
An optional numeric for the number of thread. If this is unset, detecte thread.<br>
#### QQ
logicals. If TURE, Q-Q plot would be drawn. True by default.
#### Manh
logicals. If TURE, Manhattan plot would be drawn. True by default.


## 4. Output

Here is an example of the header and the first 3 rows for the output file:

CHROM|	POS|	ID|	REF|	ALT|	A1|	TEST|	OBS_CT|	BETA|	SE|	T_STAT|	P|	ERRCODE
---- | ----- | ------ | ------| ------| ------| ------| ------| ------| ------| ------| ------| ------
1|	10390|	S1_10390	|G|	A|	A|	ADD|	2648|	-0.00784112|	0.238845|	-0.0328293	|0.973813|	|.
1|	10590|	S1_10590	|T|	A|	A|	ADD|	2648|	-0.202364|	0.249746|	-0.810281	|0.417852|	|.
1|	128373|	S1_128373|	C|	T|	T|	ADD|	2648|	0.033819|	0.124565|	0.271498	|0.78603|	|.
…

In addition to the above file, an output file named “QTNs” that includes QTN candidates exacted by Bonferroni threshold is generated from **HiGLMM** function. If joint analysis is implemented, an output file named “jointQTNs” that displays candidate QTNs from joint analysis is generated in addition.


## 5. Example
```
library(HiGLMM)
library(BEDMatrix)
library(data.table)
library(parallel)
library(snow)

setwd("./example")
plinkfilename <- "geno"
data <- Data_HiGLMM(plinkfilename)
HiGLMM(data)
```
