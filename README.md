# Hi-GLMM -Early Access

## 1. Getting started
####	Downloading Hi-GLMM
HiRRM can be downloaded https://github.com/RunKingProgram/Hi-GLMM. It can be installed as a regular R package.
####	Installing Hi-GLMM
Hi-GLMM links to R packages Rcpp, RcppArmadillo, RcppEigen, snow, parallel,data.table, nlme and BEDMatrix. These dependencies should be installed before installing Hi-GLMM. In addition, **Hi-GLMM requires gemma software**. Here is an example for installing Hi-GLMM and all its dependencies in an R session(assuming none of the R packages other than the default has been installed):
```
install.packages( c( "Rcpp", "RcppArmadillo", "RcppEigen", "snow", "parallel", "data.table", "BEDMatrix" ), repos = "https://cran.r-project.org/" )
system( “R CMD install HiGLMM_v0.9_MacOS.tgz” )
```
## 2. Main functions
The current version of HiRRM includes two main functions:
```
gdata = Data_HiGLMM(filename, h2 ,ebv = NULL) 
HiGLMM(gdata,Test=c("Jiont","Separate") ,thread=NULL,QQ=F,Manh=F)
```
#### Arguments
#### filename
An object class of character: the filename before the suffix of plink files. The three plink file must have a same filename, for example, “filename.bed”, “filename.bim” and “filename.bam”.
#### h2
An object class of numeric: Heritability will be used for estimating breeding values. Must provide, if ebv = NULL.
#### ebv
Estimated breeding values. NULL by default.
#### gdata
An object class of list generated from the Data_HiGLMM function.
####Test

An optional for association test, a test at once or joint analysis. You can choose “Separate” for a test at once and “Joint” for further joint analysis based on the result of “Separate”.

####QQ

logicals. If TURE, Q-Q plot would be drawn.

####Manh

logicals. If TURE, Q-Q plot would be drawn.


## 3.Example
```
library(HiGLMM)
library(parallel)
library(BEDMatrix)
library(data.table)
library(snow)
library(RcppArmadillo)


setwd("./example")
gdata = Data_HiGLMM("example", 0.5) 
HiGLMM(gdata)
```

