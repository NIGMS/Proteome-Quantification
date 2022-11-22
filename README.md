<img src ="images/Logo.jpg" alt ="nf-core" width="500" height="500">

## Proteomics Data Analysis Overview

This document outlines the essential steps in the process of analyzing proteomics data for the NIGMS National Resource for Quantitative Proteomics, and recommends commonly used tools and techniques for this purpose. It is assumed in this document that the experimental design is simple and that differential expression is being assessed between 2 experimental conditions, i.e. a simple 1:1 comparison, with some information about analyzing data from complex experimental designs. The focus of the SOP is on Tandem Mass Tag multiplex designs as well as Data Independent Acquistion data. This document describes the Data preprocessing, normalization, and differential abundance analysis. The minimum recommended biological replicates for each sample condition is 5. The number of replicates should be increased for more complex study designs.  

#### Note: This notebook uses simple base R plots. These can be modified to learn how to build better publication quality plots using R.

### Basic Steps 
1. Database search using Mascot, MaxQuant, or Prosit/EncylopeDIA
2. Assess the sample variance, biological replicate correlation, and data distributions using ProtieNorm
3. Perfom data normalization using the method with the lowest variance and highest intra-group correlation. For the majority of cases, VSN and Cyclic Loess have performed well. 
4. Plot quality control figures such as PCA and clustered dendrograms to check for outlier samples. These plots will give an indication of the effect size in the data. How many proteins do we expect to be differenitally expressed? 
5. Set up the limma model and run analysis. The model should consider factors such as batch, sex, age, if the samples are paired, etc. 
6. Plot the results using Volcano and/or MD plots. 

<img src ="images/WorkFlow_figure.png" alt="workflow" width="700" height = "700">

### Glossary of Terms


<b> MaxQuant: </b> a quantitative proteomics software package designed for analyzing large mass-spectrometric data sets. It is specifically aimed at high-resolution MS data. Several labeling techniques as well as label-free quantification are supported. MaxQuant is freely available at maxquant.org

<b> Tandem Mass Tag (TMT):</b> Thermo Scientific Tandem Mass Tag Reagents are designed to enable identification and quantitation of proteins in different samples using tandem mass spectrometry (MS). All mass tagging reagents within a set have the same nominal mass (i.e., are isobaric) and chemical structure composed of an amine-reactive NHS ester group, a spacer arm (mass normalizer), and a mass reporter. The standard tandem mass tag (TMT) labeling kits and reagents enable multiplex (6-plex to 11-plex) relative quantitation using high-resolution MS for samples prepared from cells or tissues.

<b> Multinotch MS3: </b> We fragment the aggregate MS3 precursor population (i.e., MultiNotch MS3) to produce a reporter ion population that is far more intense than the population we would have produced had we only fragmented a single MS2 ion. At the same time, we maintain the selectivity of the standard MS3 method by carefully defining the isolation notches of the SPS isolation waveform to ensure high isolation specificity of the target MS2 fragment ions.(McAlister et al. 2014)

<b> Data-dependent acquistion (DDA): </b> Only selected peptides are further fragemented during the second stage of tandem MS. These selected peptides are chosen within narrow range of mass-to-charge (m/z) signal intensity. Typically, the precursors of highest abundance, "top N" precursors, are selected for further analysis. MS/MS data acquistion occurs sequentially for each peptide. The resulting data is searched using existing databases. Allows relative quantification of peptides between samples. Challenges: DDA can contain "gaps" where peptides have been identified in some samples only. Low-abundance peptides are under-represented. 

<b> Data Independent Acquistion (DIA): </b> the mass spectrometer systematically acquires MS/MS spectra irrespective of whether or not a precursor signal is detected. All peptides are fragmented and analyzed during the second stage of tandem MS. MS/MS spectra are acquired either by fragmenting all ions that enter the mass spectrometer at a given time, called broadband DIA, or by sequentially focusing on a narrow m/z window of precursors and fragmenting all precursors detected within that window. MS/MS data acquistion occurs in parallel across peptides. Resulting MS spectra are highly multiplexed!  

The DIA workflow has been adopted from Brian Seerly's group. 

"Typically tens to hundreds of biological samples are processed and analyzed using LC-MS/MS in quantitative proteomics experiments.  These runs can be searched using either a typical DDA spectrum library-based workflow or a pure DIA workflow using PECAN, or spectrum-centric search methods based on DIA-Umpire or Spectronaut Pulsar. Results from runs dedicated to peptide detection are formed into a DIA-based chromatogram library. In a chromatogram library, we catalog retention time, precursor mass, peptide fragmentation patterns, and known interferences that identify each peptide on our instrumentation within a specific sample matrix. Furthermore, we report the development EncyclopeDIA, a library search engine that takes advantage of chromatogram libraries, and we demonstrate a substantial gain in sensitivity over typical DIA and DDA workflows. "


<b> Normalization: </b> to remove technical and biological sources of unwanted variation

<b> Missing Values: </b> a protein with a zero abundance indicates the protein was not identified in that sample 

<b> Batch effect: </b> occurs when non-biological factors in an experiment cause changes in the data produced by the experiment. Such effects can lead to inaccurate conclusions. Examples include multiple TMT batches, sex, samples that were prepared on different days, etc. 

<b> logfc: </b> estimate of the Log2 fold change corresponding to the contrast (group comparison)

<b> FDR p-value: </b> False discovery rate adjusted p-value for multiple test correction. FDR determines adjusted p-values for each test. A p-value of 0.05 implies that 5% of all <b> tests </b> will result in false positives. An FDR adjusted p-value (or q-value) of 0.05 implies that 5% of <b> significant tests </b> will result in false positives. The latter will result in fewer false positives.