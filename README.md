# TADPOLE-share
General repo for TADPOLE-wide issues, docs & files

## Some interesting info from the tadpole grand challenge google groups:

### Information on the columns in the datasets  
Here are some key ones to understand and ones we've had specific questions about:
- Column DX: This contains the clinical diagnosis. The entries specify both the current diagnosis and the baseline so, for example "MCI to Dementia" means that the current diagnosis is Dementia, while the diagnosis at the previous visit was MCI.
- Column DX_bl: This is the baseline diagnosis from the first visit of this subject.
- Column RID: the unique identifying code for a specific subject.
- Column EXAMDATE: the date as which the subject visiting the clinic and the data was acquired.
- Column ADAS13: the composite ADAS13 cognitive test score.
- Column Ventricles: the ventricle volume.

### The difference between the forecasting and the prediction dataset. 
Perhaps the easiest is ignore those terms and to think in terms of D1, D2 and D3. These are defined as follows:  
D1 - dataset for training (all data from subjects with at least two timepoints)  
D2 - subjects for which you need to provide forecasts (all available data)  
D3 - subjects for which you need to provide forecasts (same subjects as D2 but only one visit and only MRI+cognition) - this mimics a clinical trial where only limited cross-sectional data is available  

https://groups.google.com/d/msg/tadpolechallenge/2pSPXvsdQW8/Cj4mEsjrAQAJ  


### D3 age incorrect - ok to use D1_D2 to calculate current age?  
Python pandas DataFrame:  
```
dataTable_D1D2['VISITAGE'] = dataTable_D1D2['AGE'] + dataTable_D1D2['Years_bl']  
# Add VISITAGE to D3 using a Left Outer Join of D3 to D1D2 on {RID,VISCODE}, keeping only VISITAGE from D1D2  
dataTable_D3 = dataTable_D3.merge(dataTable_D1D2[['RID','VISCODE','VISITAGE']],how='outer',on=['RID','VISCODE'])  
```

https://groups.google.com/d/msg/tadpolechallenge/XW_PsaWkY1w/j8FQxBeDCwAJ

### useful scripts that we created for the PyConUK Hackathon.  
They can be found in this (https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2Fswhustla%2Fpycon2017-alzheimers-hack%2Ftree%2Fmaster%2Fnotebooks&sa=D&sntz=1&usg=AFQjCNEzW7lZE4pqiSJH1CQA6IjHyFmn3g) repository. In particular, it contains a useful ipython notebook that visualizes the data and cleans it up from missing values, etc ... The scripts are all based on the leaderboard datasets, but can be used for the D1/D2/D3 datasets as well.

https://groups.google.com/d/msg/tadpolechallenge/rv4u2Ab0q5o/LzU0uIHxAQAJ
