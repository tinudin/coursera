# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Useful Resources
- [ScriptRunConfig Class](https://docs.microsoft.com/en-us/python/api/azureml-core/azureml.core.scriptrunconfig?view=azure-ml-py)
- [Configure and submit training runs](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-set-up-training-targets)
- [HyperDriveConfig Class](https://docs.microsoft.com/en-us/python/api/azureml-train-core/azureml.train.hyperdrive.hyperdriveconfig?view=azure-ml-py)
- [How to tune hyperparamters](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-tune-hyperparameters)


## Summary

**In 1-2 sentences, explain the problem statement: e.g "This dataset contains data about... we seek to predict..."**
The dataset contains data from a banking institution, where marketing campaigns are tracked. The length of the dataset is 32950 datapoints. The split of positiv and negativ cases is 3692 positiv and 29258 negativ cases, meaning wether the campaign was successful for  a person or not. Data features are versatile in their characteristics and contain age, occupation and more.
**In 1-2 sentences, explain the solution: e.g. "The best performing model was a ..."**
The data was prepared by creating a one hot encoding  for categorical variables. We chose Random Sampling for the Hyperparameter tuning. For early stopping, the Bandit Policy was chosen. 


## Scikit-learn Pipeline
**Explain the pipeline architecture, including data, hyperparameter tuning, and classification algorithm.**
Pipline is as follows: Data Collection -> Data Cleasning -> creation of training split -> Hyperparameter Sampling with Random Sampler -> Model Training -> Model Testing
**What are the benefits of the parameter sampler you chose?**
As Bayesian Sampling can be computational expensive, the Random Sampler offeres a way more efficient solution to sampling. 
**What are the benefits of the early stopping policy you chose?**
Bandit is a policy based on slack/factor amoubnt and on the intervals. This policy shows to be very lightweight and efficient. 

## AutoML
**In 1-2 sentences, describe the model and hyperparameters generated by AutoML.**
AutoML produces a wide range of models with an best metric of 0.9175 delivered by Voting Ensemble Model.

 ITER   PIPELINE                                       DURATION            METRIC      BEST
    0   MaxAbsScaler LightGBM                          0:00:19             0.9145    0.9145
    1   MaxAbsScaler XGBoostClassifier                 0:00:28             0.9136    0.9145
    2   MaxAbsScaler ExtremeRandomTrees                0:00:20             0.7270    0.9145
    3   SparseNormalizer XGBoostClassifier             0:00:21             0.9137    0.9145
    4   MaxAbsScaler LightGBM                          0:00:15             0.9120    0.9145
    5   MaxAbsScaler LightGBM                          0:00:14             0.8882    0.9145
    6   StandardScalerWrapper XGBoostClassifier        0:00:16             0.9087    0.9145
    7   MaxAbsScaler LogisticRegression                0:00:21             0.9088    0.9145
    8   StandardScalerWrapper ExtremeRandomTrees       0:00:15             0.8883    0.9145
    9   StandardScalerWrapper XGBoostClassifier        0:00:16             0.9134    0.9145
   10   SparseNormalizer LightGBM                      0:00:15             0.9052    0.9145
   11   StandardScalerWrapper XGBoostClassifier        0:00:16             0.9134    0.9145
   12   MaxAbsScaler LogisticRegression                0:00:20             0.9088    0.9145
   13   MaxAbsScaler SGD                               0:00:14             0.8598    0.9145
   14   StandardScalerWrapper XGBoostClassifier        0:00:18             0.9134    0.9145
   15   SparseNormalizer RandomForest                  0:00:35             0.8188    0.9145
   16   StandardScalerWrapper LogisticRegression       0:00:17             0.9080    0.9145
   17   StandardScalerWrapper RandomForest             0:00:21             0.9005    0.9145
   18   StandardScalerWrapper XGBoostClassifier        0:00:19             0.9131    0.9145
   19   TruncatedSVDWrapper RandomForest               0:02:27             0.8236    0.9145
   20   TruncatedSVDWrapper RandomForest               0:04:28             0.8332    0.9145
   21   StandardScalerWrapper XGBoostClassifier        0:00:41             0.9143    0.9145
   22   StandardScalerWrapper LightGBM                 0:00:46             0.9114    0.9145
   23   MaxAbsScaler LightGBM                          0:00:37             0.8882    0.9145
   24   StandardScalerWrapper XGBoostClassifier        0:01:12             0.9154    0.9154
   25   StandardScalerWrapper XGBoostClassifier        0:00:41             0.8882    0.9154
   26   MaxAbsScaler LightGBM                          0:00:39             0.9086    0.9154
   27   StandardScalerWrapper XGBoostClassifier        0:01:25             0.9102    0.9154
   28   StandardScalerWrapper ExtremeRandomTrees       0:01:48             0.8882    0.9154
   29   MaxAbsScaler LightGBM                          0:00:37             0.9010    0.9154

## Pipeline comparison
**Compare the two models and their performance. What are the differences in accuracy? In architecture? If there was a difference, why do you think there was one?**
While AutoML produces networks with a performance of 0.9154, hyperdrive produces a network with an accuracy of 0.9080, meaning AutoML produces a slightly improved model. Massive improvement is the wide range of models offered and checked by AutoML.

## Future work
**What are some areas of improvement for future experiments? Why might these improvements help the model?**
Building on the pipeline so far, it would be possible to add complexity by  improving sampling using bayesian methods.

## Proof of cluster clean up
**If you did not delete your compute cluster in the code, please complete this section. Otherwise, delete this section.**
**Image of cluster marked for deletion**
image can be found in img
