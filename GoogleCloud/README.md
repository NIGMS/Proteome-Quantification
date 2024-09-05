
## *Creating a user managed notebook in GCP* 

Follow the steps highlighted [here](https://github.com/STRIDES/NIHCloudLabGCP/blob/main/docs/vertexai.md) to create a new user-managed notebook in Vertex AI. Follow steps 1-8 and be especially careful to **enable idle shutdown** as highlighted in step 7. For this module you should select **Debian 10 and R 4.2** in the Environment tab in step 5. In step 6 in the Machine type tab, select **n1-standard-4** from the dropdown box.

To clone this repository, open a Terminal window in your new instance and type `git clone https://github.com/NIGMS/Proteome-Quantification/GoogleCloud.git` This will create a directory called Proteome-Quantification. Navigate into that directory and open the tutorial notebooks to get started.

### Basic Steps 

1. Database search using Mascot, MaxQuant, or Prosit/EncylopeDIA. The example TMT data was searched using MS3 in MaxQuant. 
2. Assess the sample variance, biological replicate correlation, and data distributions using ProtieNorm (Graw et al 2021). 
3. Perform data normalization using the method with the lowest variance and highest intra-group correlation. For the majority of cases, VSN and Cyclic Loess have performed well. 
4. Plot quality control figures such as PCA and clustered dendrograms to check for outlier samples. These plots will give an indication of the effect size in the data. How many proteins do we expect to be differentially expressed? 
5. Set up the limma model and run analysis. The model should consider factors such as batch, sex, age, if the samples are paired, etc. 
6. Plot the results using Volcano and/or MD plots. 

