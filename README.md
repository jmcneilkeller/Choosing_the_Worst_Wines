# Choosing the Worst Wines

## 1. The question

It's been proven time and time and time again that most human beings aren't really that good at differentiating between good and mediocre wine, or even between types of wine. If you are the average restaurant owner, it stands to reason that all you really need to do is avoid the detectably bad wines and anything else you buy should be generally fine.

Our question then is: Can we determine detectably bad wines from their chemical composition?

## 2. The data

For this experiment red wines and white wines were examined separately as they are created using different processes and generally have different compositions. The relevant data:

Red wine:

* 1599 observations initially.
* 1347 after cleaning.
* Quality scores ranged between 3-8.
* 61 ‘poor’ quality wines

White wine:

* 4898 observations initially.
* 3954 after cleaning.
* Quality scores ranged between 3-9.
* 171 'poor’ quality wines

For this experiment wines rated as either a 3 or 4 were considered 'poor'.

In order to correct the major class imbalance (see below), I upsampled both datasets using SMOTE. The minority class represented 15% of each of the final datasets after upsampling. 

![](https://github.com/jmcneilkeller/Choosing_the_Worst_Wines/blob/master/images/class_imbalance.png)

## 3. Features

### Sulfure dioxide

Sulfur dioxide is added to wines in order to reduce oxidation and to create an unhealthy environment for yeast so that the wine retains its sugars. A wine with a higher pH will require more SO2. However, if too much sulfur dioxide is added to the wine, it can noticeably impact the taste.

I engineered features to measure the amount of Molecular SO2 (the SO2 that is active in fighting yeast and oxidation) and Bound SO2 (inert SO2) in addition to the existing Free SO2 and Total SO2 features.

Free sulfur dioxide distribution:

![](https://github.com/jmcneilkeller/Choosing_the_Worst_Wines/blob/master/images/so2.png)

### pH

Both red and white wines have optimal pH values.

* 3.0-3.4 optimal for white
* 3.3-3.6 optimal for red

I binned wines with those values separately in order to hopefully weed out wines without those optimal values.

### Alcohol

Based on my research, the alcohol content of a wine may be a strong indicator of quality. I binned wines into low, medium and high alcohol content.

## 4. Results

Given that I was aiming to find the worst wines, I optimized my models towards a higher recall score with the idea of minimizing false negatives. My best models are below:

Red
* Logistic Regression w/Polynomial Features
  * Accuracy: .79
  * Recall: .62

White
* Logistic Regression w/Polynomial Features
  * Accuracy: .83
  * Recall: .70

The results are not quite as I had hoped. I believe the major problem is the dataset class imbalance. I hope to improve this model with additional data. 

Final confusion matrices:

![](https://github.com/jmcneilkeller/Choosing_the_Worst_Wines/blob/master/images/confusion_matrices.png)
