### Tagger Evaluation - Scripts

The Python scripts in this folder were used to implement our evaluation of the RCT Tagger. These are the 5 steps in our evaluation of the RCT Tagger tool as shown in the following chart. In order to run the scripts, please make sure you have Python installed (version 3.1 or above recommended). Data files that were created in each step are described in detail at: https://github.com/infoqualitylab/Tagger_Evaluation/tree/master/Data

![Main steps of the RCT Tagger evaluation](https://github.com/infoqualitylab/Tagger_Evaluation/blob/master/Images/TaggerEvaluation_MainSteps.png.PNG)

#### Step 1: Select a sample of Cochrane reviews
Our sampling strategy was to first take a representative sample consisting of 15% of the total reviews in the full Cochrane review dataset, and second to limit to reviews that only included RCT studies, according to the Cochrane reviews’ inclusion criteria. 

The Python script **"Step1.1_Randomised_sampling.ipynb"** was used to randomly select 15% of total 7158 reviews from the original dataset, resulted into 895 reviews. We then annotated these reviews' inclusion criteria and selected the ones that only included RCTs, resulting in the final 570 reviews that was used in our evaluation. 

Note: In this step, the script randomly selected the reviews. Therefore, rerunning the script might result in a different set of data compared with the data that we used in our evaluation study. 

#### Step 2: Extract article metadata
The Python script **"Step2.1_Extract_MetaData_IncludedStudies.ipynb"** was used to extract metadata about each included article from each sampled review. The script read XML files of the reviews and extracted information of the included articles in each review and saved into an Excel file for futher usage. 

#### Step 3: Collect PubMed identifiers (PMIDs) for articles
To collect PubMed identifiers for the articles, we queried the PubMed API (https://www.ncbi.nlm.nih.gov/home/develop/api/) for PMIDs matching each article’s metadata, which included two sub-steps:

Sub-step 1: We used the ECitMatch API because it determines exact matches between a citation string and a PMID. For each article, we input to ECitMatch its publication year, journal, volume, and page numbers. The Python script **"Step3.1_Get_PMIDs_ECitMatchAPI.ipynb"** was used to run ECitMatch API in order to get PMIDs of included articles in our dataset. 

Sub-step 2: For articles not matched by the ECitMatch API, we used the ESearch API because it returns a list of PMIDs as results of a single text query. Input was the title, the first author and the publication year. The Python script **"Step3.2_Get_PMIDs_ESearchAPI.ipynb"** was used to run ESearch API in order to get PMIDs of the included articles that were unsuccessfully matched PMIDs in the first sub-step.

Sub-step 3: For each of articles that had PMIDs returned by the API, we compared its title and abstract collected from the original Cochrane Review against the PubMed API. This resulted in two lists: a list of articles that had a PMID mapping error(which we excluded); and a list of articles that have PMID matches. The later one is used as input of the RCT Tagger to get RCT prediction scores.The Python script **"Step3.3_PMIDs_Mapping_Errors_Checking.ipynb"** was used to collect titles/abstracts of the articles from PubMed database and compared with those from the original Cochrane Reviews.

#### Step 4: Get RCT Tagger’s Predictions
We ran the RCT Tagger on the PMIDs retrieved in step 3.

#### Step 5: Error analysis
We conducted an error analysis on the articles that given low scores by the RCT Tagger. 

Sub-step 5.1: We conducted error analysis of 44 articles that were given low scores by the RCT Tagger but marked with "Randomized Controlled Trial" publication type on PubMed. The Python script **Step5.1_Metadata_Analysis_of_Low_Scored_Articles.ipynb** was used to collect metadata of the articles given low scores by the RCT Tagger, including: their PubMed publication type, title, authors. We also manually collected their full-text to do the error analysis. 

Sub-step 5.2: We conducted error analysis of 254 articles that were given low scores by the RCT Tagger without "Randomized Controlled Trial" publication type on PubMed. The Python script **Step5.2_Primary_Secondary_Studies_Analysis_Low_Scores_Articles.ipynb** was used to collect information about included studies in which the articles come from, including: characteristics of the included studies, whether the study is primary or secondary. 


