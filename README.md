# CS523 Final Project Detect AI-generated models on encrypted images

## Environment Dependencies
* Python (Version 3 or higher)
* Packages:
* * sklearn
  * pycaret
  * xgboost
  * lightgbm
  * seaborn
  * pandas
  * numpy
  * imblearn

## My Models
I used a stacked model of knn naive bayes, and xgboost for my best model. First, I ran an automl program using the pycaret that figured out which models had the highest accuracy and F1 score.

![CS523_dataset_ml_table](https://github.com/bmahabirbu/CS523/assets/56164556/651b3c1f-5df0-4e4a-aa58-d0951c9fd1fe)

From here I picked knn and xgboost and use naive bayes as a midpoint feature extraction as it had the highest recall value.

From here I tried ensembling the models in a voting class, stacking them, etc, to see which had the highest accuracy. The stacked model came out ontop.
Afterwards, I used pycaret to tune each model's hyperparameters using the built-in tune_model function which uses random sampling to boost my accuracy even more.


Accuracy: 89.71%
fscore: 77.87%

![db647099-13f7-4e4b-ae48-84e6c04515c3](https://github.com/bmahabirbu/CS523/assets/56164556/2f9e9639-a391-43b3-a3a1-e73ab58bdb44)
![81953c64-c80c-4a0c-915e-8e92e1c828c6](https://github.com/bmahabirbu/CS523/assets/56164556/5cf46589-1dad-43bd-9c58-b0afa465bd4b)
![4a781622-c111-4943-9794-9befc18f9e3d](https://github.com/bmahabirbu/CS523/assets/56164556/d51197b1-6c22-46f2-bd27-e38dfd8999b7)
![9c298fad-7d8d-4d95-85d5-1ce1f88136d9](https://github.com/bmahabirbu/CS523/assets/56164556/c8017634-664c-4435-a914-87bf8809cd9a)
![5f8c78ae-a003-4018-9e0e-0e428bcd6a51](https://github.com/bmahabirbu/CS523/assets/56164556/269643fc-e493-44eb-84d9-6c3ac292ff9e)


After playing around with this my accuracy hit a plateau. In the next section ill explain the different steps I took to try and increase my accuracy even more. Sadly, none of what I did ended up working but it's worth noting the plethora of different techniques I tried.

## Data Augmentation

I first noticed that the data was imbalanced

![e7cf7b39-b738-4480-8ed1-b78d197fe0c4](https://github.com/bmahabirbu/CS523/assets/56164556/0e7f9af2-24db-4725-b869-5767ee834105)

I tried oversampling the data, smart oversampling using SMOTE, undersampling the data, and a combination of all.

Here is an example of oversampling

![70393b39-59a2-47fa-bda3-34e0bc021afc](https://github.com/bmahabirbu/CS523/assets/56164556/9f0a53ba-af13-4078-9f66-6b09cc676fa8)

All in all sampling the data in this way made my accuracy much worse. This shows that the data is quite unique and cant be reproduced using normal means.

Along those lines I came across a paper that stated histograms-of-oriented-gradients feature extraction would still be able to extract features even on encrypted images using block-based encryption. I had no idea what encryption the company used to encrypt the images but it was worth a shot.
https://arxiv.org/pdf/1904.12434.pdf

Even though my overall accuracy went down it was interesting to note that SVM which the paper used increased the accuracy by 5%

