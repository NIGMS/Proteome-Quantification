# Google Cloud Proteomics Training Tutorial

## Proteomics Data Analysis Overview

This notebook outlines the essential steps in the process of analyzing proteomics data and recommends commonly used tools and techniques for this purpose. It assumes a simple experimental design for differential abundance including two experimental conditions such as cancer vs normal. The training data provided utilized TMT10plex multiplex design with MS3 data acquistion. This notebook describes mass spectrometry and statistical terminology for data preprocessing, normalization, and differential abundance analysis. Note: This notebook uses simple base R plots. These can be modified to learn how to build better publication quality plots using R. 

## Table of Contents

<a href="#requirements">Requirements</a></br>
<a href="#getting-started">Getting Started</a></br>
<a href="#funding">Funding</a></br>
</br>

## <a name="requirements">Requirements</a>

This tutorial was designed to be used on cloud computing platforms, with the aim of requiring nothing but the files within this github repository.
The Jupyter Notebook file can run on Google Cloud Platform, Amazon Web Service, and Microsoft Azure provided the R packages are installed. The Notebook can be launched using NIH STRIDES training module and therfore requirements should only require access NIH STRIDES resources.


This tutorial will cost you just less than $1.00 assuming a n1-standard-4 machine, and assuming you delete the virtual machine after you finish the tutorial.

## <a name="getting-started">Getting Started</a>

### Basic Steps 

1. Database search using Mascot, MaxQuant, or Prosit/EncylopeDIA. The example TMT data was searched using MS3 in MaxQuant. 
2. Assess the sample variance, biological replicate correlation, and data distributions using ProtieNorm (Graw et al 2021). 
3. Perfom data normalization using the method with the lowest variance and highest intra-group correlation. For the majority of cases, VSN and Cyclic Loess have performed well. 
4. Plot quality control figures such as PCA and clustered dendrograms to check for outlier samples. These plots will give an indication of the effect size in the data. How many proteins do we expect to be differenitally expressed? 
5. Set up the limma model and run analysis. The model should consider factors such as batch, sex, age, if the samples are paired, etc. 
6. Plot the results using Volcano and/or MD plots. 

## <a name="funding">Funding</a>

Funded by National Resource for Quantitative Proteomics NIH/NIGHMS R24GM137786.
