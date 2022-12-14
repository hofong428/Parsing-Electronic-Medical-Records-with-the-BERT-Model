# Parsing-Electronic-Medical-Records-with-the-BERT-Model  
We hope to predict whether the patient will be readmitted within the next 30 days from the EMR during hospitalization.  

**Problem Description**  
We hope to predict whether the patient will be readmitted within the next 30 days from the clinical records of the patient during hospitalization. This prediction can assist doctors to better choose treatment options and evaluate surgical risks. It is not uncommon in clinic that the treatment methods are common but the prognosis is difficult to control and manage. Joint replacement surgery, for example, has achieved great clinical success as a definitive treatment for diseases such as osteoarthritis in the elderly, but complications associated with the surgery and resulting readmissions are not uncommon.  

The patient's own factors such as heart disease, diabetes, obesity and other conditions can also increase the risk of readmission after joint replacement. As the population undergoing joint replacement surgery gets older and in poorer health, there are more complications and an increased risk of hospital readmission.    

Through the relevant records of electronic medical records, it is observed that for certain diseases or operations, the risks of patients who are readmitted within 30 days are significantly increased in all aspects. Therefore, the case of re-hospitalization with the same reason as the previous hospitalization, and the interval between the previous discharge and the next admission was not more than 30 days was considered as the same hospitalization, and the model was trained to try to solve this problem.  

**Data selection and data cleaning**  
Selected from the Medical Information Mart for Intensive Care III data set, also known as MIMIC-III, is a multi-parameter intensive care database jointly developed and maintained by MIT, Harvard Medical School BID Medical Center, and Philips Medical under the funding of NIH.  
   
   We deployed the data in Postgre SQL while conducting experiments.  
   
   First, take out all the data from the admission table, calculate the time interval for the next occurrence of the same subject_id for each record, if it is less than 30 days, add the label Label=1 to the record, otherwise Label=0. Then calculate the length of the hospitalization (discharge date - admission date), and draw samples with length of hospitalization > 2. The HADM_ID of all the samples extracted above are randomly allocated according to the ratio of 0.8:0.1:0.1 to form a training set, a verification set and a test set.   
   
   Afterwards, the text content of each data set (that is, the TEXT column in the noteevents table) is obtained from the noteevents table according to the previously assigned HADM_ID. The organized training set, verification set and test set all contain three columns, namely TEXT (text content), ID (ie HADM_ID), Label (0 or 1), here we provide a clean test data for your use.    

**pre-trained model**  
The pre-trained model used in the original project. Based on BERT training. The BERT model has a milestone significance in the field of NLP (Natural Language Processing). On October 11, 2018, Google released the paper "Pre-training of Deep Bidirectional Transformers for Language Understanding", which successfully achieved state of the art results in 11 NLP tasks and won praise from the natural language processing community. The BERT model has achieved good results in many fields such as text classification and text prediction.  

**The principle of the BERT algorithm is mainly composed of two parts:**  
- In the first step, the expressions are learned through unsupervised pre-training on a large unlabeled corpus.  
- Second, the pretrained model is fine-tuned in a supervised manner using a small amount of labeled training data for various supervised tasks.  
The ClinicalBERT model fine-tunes the BERT model based on labeled clinical records to obtain a model that can be used for text analysis in the medical field.
