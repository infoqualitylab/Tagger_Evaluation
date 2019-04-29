 ### These are the 5 steps in our evaluation of the RCT Tagger tool as shown in the following chart:

![Main steps of the RCT Tagger evaluation](https://github.com/infoqualitylab/Tagger_Evaluation/blob/master/Images/TaggerEvaluation_MainSteps.png)

 #### Step 1: Select a sample of Cochrane reviews
Our sampling strategy was to first take a representative sample consisting of 15% of the total reviews in the full Cochrane review dataset, and to second limit to reviews that only included RCT studies, according to the Cochrane reviews’ inclusion criteria. 

The Python script "Step1_Randomised_sampling" was used to randomly select 15% of total 7158 reviews from the original dataset, resulted into 895 reviews. We then annotated these reviews' inclusion criteria and selected the ones that only included RCTs, resulted in the final 570 reviews that was used in our evaluation. 

