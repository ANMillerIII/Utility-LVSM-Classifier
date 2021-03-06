
# Disclaimer
Utility specific information regarding equipment and maintenance programs has been redacted, rendering this view-only.

## Purpose
The use case is classification of electric plant (utility) equipment failure mitigation strategies into general categories to identify trends and deficiencies.

## Background

This model classifies recods in the free-text 'Mitigation' field of a plant equipment database (71,000 records) into based on 'Mitigation' strategy type. Records are binned into one or multiple of the following classes:

- maintenance	
- operational	
- physical_barrier	
- design_and_engineering	
- supply_chain
- unknown

The NLP classifier applies a Linear Support Vector Classification (SVC) algorithm (https://scikit-learn.org/stable/modules/generated/sklearn.svm.LinearSVC.html).

LVSC was selected based on trials using a number of text-classification algorithms, including:

- Random Forrest
- Naive Bayes
- Linear Regression

Moreover, this classifier applies a multi-label, "One vs Rest" (also known as 'binomial classifiication') strategy, which iteratively applies a seperate LVSM classifier for each label.

## Classifier Setup

1. Clone the repository

`git clone https://github.com/ANMillerIII/LVSM.git`

2. Initialize and activate vitual environment 

`py -m venv venv`

`./venv/Scripts/activate`

3. Install dependencies

`py -m pip install requirements.txt -r`

4. Switch to "LVSM" directory

`cd LVSM`

## Run Classifier

To run the 'Mitigation' classifier

`py ./1_mitigation/mitigation_model.py`

Prediction output will be in the respective 'out' directories

## Limitations

1. 'train_set' data set is used based on naive string matching with some oversight. This should be improved by manually classifying a greater sample of 'Mitigation' fields by hand.
2. Accuracy is not a meaningful metric for the 'apply_set' data, since the model is used to make predictions (i.e., must spot check manually)
3. Foreign-language entries are classified with low fidelity due to lack of manual classification.
4. 'train_set' data (3,569 records) are not classified by NLP, but rather string-matching/manually with inherent biases.
