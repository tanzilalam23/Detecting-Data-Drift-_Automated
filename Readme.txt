Readme

Abstract:

Data drift can be described as a change in the distribution of unseen input data when compared to the data used in training. This is a concerning problem as we gear up to deploy our pipeline in production. We want to ensure that the reports processed by our pipeline during production are similar to the surgical pathology reports we used in training. Processing a report from a different domain e.g. radiotherapy carries a high risk of poor quality abstraction, which may lead to incorrect clinical inference and in the end, endanger the patient. Data drift may also arise due to differences in the layout of the reports. The aim of the project is to find the data drfit of the unseen report when compared to the training dataset. 

Workflow:

The project mainly design to take in the OCR reports and convert it into text file which is then furthere processed and operated to find the data drift. Pipeline can be describe as, first call the analysis_module which will import datadrift_module, then in datadrift_module we import preprocessing_module, going forward we use the threshold, train and model which is trained and analysis from the train_module.

Steps/ Operation:

In this section I will describe the responsibility and features of each or all four modules.

1. tain_module:

This module is created to find and save the threshold, model, train embeddings and train vecotrs of the TF-IDF and Word2Vec vecotorization. Here the mention variables are calculated between the train and validation dataset. Validation dataset is nothing, rather just a train- test split of train dataset. That is, train dataset is splitted randomly into 80% (which is assign as train embddings) and 20%(which is assigned as validation/ test embddings). Further, six variables are calculated accrodingly:

a. In w2v function, the word2vec vectorizer model is calculated and saved in the model variable; going forward with that model the train_embeddings are calculated and saved. Henceforth we calculate the cosine mean similartiy and find the value of 10th percentile to assign that value as threshold value and saved in the varibable threshold(w2v).

b. In tfidf function, tfidf vectorizer calculated and saved in the variable vectorizer(tfidf); going forward with that vectorizer we are fitting and transforming the training dataset and saving it into a variable train(tfidf). Henceforth we calculate the cosine mean similartiy and find the value of 10th percentile to assign that value as threshold value and saved in the varibable threshold(tfidf).

Now these six variable will invoked by the datadrift module to find the datadrift with the unseend dataset.

2. preprocessing_module: 

This module is designed so that it can be used by train_module to preprocess the training dataset and it is also used in the datadrift module to preprocess the unseen dataset. The preprocessing module comes with a striaght forward approch to preprocess the text brfore the operation is done to it. 

Please Note: Don't forget to modify the preprocessing module as per your requirements.

3. datadrift_module:

This is the main module where datadrift is been calculated. a predict_data_drift function is created in order to take two arguments, unseen dataset and a boolean result whether you want to calculate tfidf or word2vec. 

Firstly the unseen dataset is preprocessed and stored in the df_unseen dataframe. Then an if statement is called that if tfidf == 1 then;

tfidf block of code is activated which will call the vectorizer, train(tfidf), and threshold(tfidf) which was saved by train_module and then data drift is calculate with the unseens dataset.

if tfidf is null or zero then word2vec block of code is activated and it calls its variable and calcultes the word2vec datadrift with the unseen dataset.

At the end, message is displayed for each of the unseen documents whether data drift exists or not with the training document. 

4. analysis_module:

This module is simply created for the analysation of results. It is importing the datadrift_module and predict_data_drift function is called and the parameters is given (i,e,; the location of the unseen dataset) to find the results. 