  
**Evaluation Metrics**  
**for Classification**

*A Beginner Friendly Guide*

Notes prepared for learners starting out in machine learning

# **1\. Why Evaluation Metrics Matter**

When you build a classification model, you need a way to check how well it is doing. Simply looking at the predictions is not enough. Evaluation metrics give you numbers that describe the quality of a model in different ways. Different metrics highlight different strengths and weaknesses, so it helps to understand more than one.

Classification means the model is trying to sort things into categories, for example deciding whether an email is spam or not spam, or whether a patient has a disease or not.

# **2\. The Confusion Matrix**

Before understanding most metrics, it helps to understand the confusion matrix. It is a simple table that compares what the model predicted against what actually happened.

|  | Predicted Positive | Predicted Negative |
| :---- | :---: | :---: |
| **Actual Positive** | True Positive (TP) | False Negative (FN) |
| **Actual Negative** | False Positive (FP) | True Negative (TN) |

## **The four possible outcomes**

* True Positive (TP): the model predicted positive and it was actually positive

* True Negative (TN): the model predicted negative and it was actually negative

* False Positive (FP): the model predicted positive but it was actually negative (a false alarm)

* False Negative (FN): the model predicted negative but it was actually positive (a miss)

# **3\. Core Metrics**

## **3.1 Accuracy**

Accuracy tells you the percentage of predictions the model got right, out of all predictions made.

*Accuracy \= (TP \+ TN) / (TP \+ TN \+ FP \+ FN)*

Accuracy is easy to understand, but it can be misleading when the classes are imbalanced. For example, if 95 percent of emails are not spam, a model that always predicts not spam will have 95 percent accuracy without being useful at all.

| Use it when Your classes are roughly balanced and every type of mistake costs about the same, for example predicting whether a coin toss image shows heads or tails. | Avoid it when Your classes are imbalanced, for example detecting a rare disease that only 1 in 1000 patients have. A model that always says healthy would score 99.9 percent accuracy while missing every real case. |
| :---- | :---- |

## **3.2 Precision**

Precision answers the question: of everything the model labeled as positive, how many were actually positive?

*Precision \= TP / (TP \+ FP)*

High precision means the model does not raise many false alarms. This matters when the cost of a false positive is high, for example flagging a genuine transaction as fraud.

| Use it when False positives are costly or disruptive, for example marking a genuine email as spam so the user misses an important message, or flagging a legitimate transaction as fraud and blocking a customer's card. | Avoid it when Missing a positive case is far more costly than a false alarm, for example missing a cancer diagnosis just to keep false alarms low. Precision alone ignores how many real cases were missed. |
| :---- | :---- |

## **3.3 Recall (also called Sensitivity)**

Recall answers the question: of all the actual positives, how many did the model correctly find?

*Recall \= TP / (TP \+ FN)*

High recall means the model rarely misses a true positive. This matters when missing a positive case is costly, for example failing to detect a disease.

| Use it when Missing a positive case is dangerous or expensive, for example missing a cancer diagnosis in a screening test, or letting a real security threat pass through undetected. | Avoid it when False alarms are costly and need to stay low, for example a cancer screening test that flags every patient as high risk just to avoid missing any real case, leading to unnecessary stress and follow up tests for healthy people. |
| :---- | :---- |

## **3.4 Specificity**

Specificity is like recall, but for the negative class. It answers: of all the actual negatives, how many did the model correctly find?

*Specificity \= TN / (TN \+ FP)*

| Use it when Correctly ruling out negative cases matters a lot, for example confirming a healthy patient is truly healthy so they are not sent for unnecessary and costly further testing. | Avoid it when Your main concern is catching positive cases, for example detecting cancer. A model can have high specificity by rarely raising alarms, while still missing many actual cancer cases. |
| :---- | :---- |

## **3.5 F1 Score**

Precision and recall often trade off against each other. The F1 Score combines both into a single number using their harmonic mean, so it is useful when you want one balanced measure.

*F1 Score \= 2 x (Precision x Recall) / (Precision \+ Recall)*

The F1 Score is especially helpful when the classes are imbalanced and accuracy alone is not trustworthy.

| Use it when You need one single score that balances precision and recall, for example evaluating a spam filter where both missed spam and blocked real emails matter. | Avoid it when You care a lot more about one of precision or recall specifically, for example in cancer screening where missing a real case (recall) matters far more than a false alarm. F1 treats both as equally important, which can hide that imbalance. |
| :---- | :---- |

## **3.6 Macro-F1 Score**

The F1 Score above works for a single class, such as positive versus negative. When there are more than two classes, for example classifying an image as a cat, dog, or rabbit, you need a way to combine the F1 Scores of every class into one number. Macro-F1 does this by calculating the F1 Score separately for each class, then taking the plain average across all classes.

*Macro-F1 \= (F1 for class 1 \+ F1 for class 2 \+ ... \+ F1 for class n) / n*

The word macro means every class counts equally, no matter how many examples it has. This is different from a weighted average, which would give larger classes more influence over the final score.

| Use it when You have multiple classes and want every class, including rare ones, to matter equally, for example classifying rare diseases where each disease type is equally important even if one type is much rarer than another. | Avoid it when Your classes are very imbalanced and the rare classes are not actually a priority, since Macro-F1 can look low even when the model performs well on the classes that matter most to you. |
| :---- | :---- |

# **4\. Quick Reference Table**

| Metric | What it tells you | Formula |
| :---- | :---- | ----- |
| Accuracy | How many predictions were correct overall | (TP+TN) / Total |
| Precision | Of all predicted positives, how many were actually positive | TP / (TP+FP) |
| Recall (Sensitivity) | Of all actual positives, how many were correctly found | TP / (TP+FN) |
| Specificity | Of all actual negatives, how many were correctly found | TN / (TN+FP) |
| F1 Score | Balance between precision and recall | 2 x (P x R) / (P+R) |
| Macro-F1 | Average F1 across all classes, each weighted equally | Sum of class F1 / n |
| ROC-AUC | How well the model ranks positives above negatives overall | Area under ROC curve |
| PR-AUC | How well the model keeps precision high across recall levels | Area under PR curve |

# **5\. A Few More Useful Metrics**

## **5.1 ROC Curve**

ROC stands for Receiver Operating Characteristic. The ROC curve is a graph that shows how the true positive rate (recall) and the false positive rate change together as you slide the decision threshold from strict to loose. Each point on the curve represents the model's performance at one particular threshold.

* The x-axis shows the false positive rate: how often the model wrongly flags a negative case as positive

* The y-axis shows the true positive rate: how many actual positives the model correctly finds

* A curve that hugs the top left corner means the model separates the two classes well at many thresholds

* A curve that sits close to the diagonal line means the model is close to guessing randomly

| Use it when You want to see how a model's true positive rate and false positive rate trade off as the decision threshold changes, for example deciding how strict a fraud alert system should be. | Avoid it when You need a single number to quickly compare models, since the curve itself is a visual rather than one score. Use ROC-AUC below for that. |
| :---- | :---- |

## **5.2 ROC-AUC**

ROC-AUC stands for Area Under the ROC Curve. It takes the whole ROC curve and reduces it to a single number between 0 and 1, making it easier to compare models without reading a graph.

* An ROC-AUC of 0.5 means the model is guessing randomly

* An ROC-AUC of 1.0 means the model separates the classes perfectly

* A higher ROC-AUC generally means a better model, regardless of the threshold chosen

| Use it when You want to compare models overall or have not yet decided on a classification threshold, for example choosing between two candidate models before deciding how strict the cutoff should be. | Avoid it when The classes are heavily imbalanced, for example a rare fraud detection task where ROC-AUC can look high even if the model performs poorly on the rare fraud cases. PR-AUC below is usually more informative here. |
| :---- | :---- |

## **5.3 PR-AUC**

PR-AUC stands for Area Under the Precision-Recall Curve. Instead of plotting true positive rate against false positive rate like ROC does, the precision-recall curve plots precision against recall at different thresholds. PR-AUC summarizes that curve into a single number between 0 and 1\.

* A PR-AUC close to 1.0 means the model keeps precision high even as recall increases

* A PR-AUC close to the proportion of positives in the data means the model is close to guessing randomly

* PR-AUC focuses only on how the model handles the positive class, and ignores true negatives entirely

| Use it when Your classes are heavily imbalanced and you mainly care about the positive class, for example detecting a rare disease or rare fraud, where true negatives are plentiful and not very informative. | Avoid it when Your classes are roughly balanced and you also care about how well the model identifies true negatives, since PR-AUC does not take true negatives into account at all. ROC-AUC is usually a better fit there. |
| :---- | :---- |

## **5.4 Log Loss**

Log Loss, short for logarithmic loss, measures how well the predicted probabilities match the actual outcomes, rather than just checking if the final label was right. It punishes confident wrong predictions more heavily than uncertain ones.

| Use it when You care about how confident and well calibrated the predicted probabilities are, for example a weather app predicting a 90 percent chance of rain, where the actual probability matters, not just a yes or no answer. | Avoid it when You only need the final predicted class, for example a simple spam or not spam label, and calibrated probabilities do not matter for your use case. |
| :---- | :---- |

## **5.5 Support**

Support simply refers to the number of actual occurrences of each class in the dataset. It is often shown alongside precision, recall, and F1 Score in a classification report so you know how much data each score is based on.

# **6\. Choosing the Right Metric**

There is no single best metric for every situation. A helpful way to decide is to think about what mistake is more costly.

* If false positives are costly, prioritize precision

* If false negatives are costly, prioritize recall

* If you need one balanced number, use the F1 Score

* If your classes are imbalanced, avoid relying on accuracy alone

* If you want to compare models across all thresholds and classes are fairly balanced, look at ROC-AUC

* If you want to compare models across all thresholds and classes are heavily imbalanced, look at PR-AUC instead

* If you have more than two classes and want every class treated equally, use Macro-F1

*Tip: Always look at more than one metric together. A single number rarely tells the whole story about how a model performs.*