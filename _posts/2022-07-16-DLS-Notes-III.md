---
layout: post
title: (Google ML Bootcamp) Notes on DLS Coursera - III
categories: [coding, ML]
---

## Course 3: Structuring Machine Learning Projects

* Satisficing and Optimizing Metric: We optimize the most important features first, then we set a threshold for the other metric to satisfy.

* Choose a dev set and a test set to reflect data you expect to get in the future and consider important to do well on. It means: similar distributions to the real world data.

* Size of the test set:  Train/dev for really small dataset (10e4-10e5)

*  Human Error is a better target to beat than reaching Bayes Error

### Error Analysis:

* Get examples that are mislabeled, check them by hand
* Count how many mismatches are there, check if the percentage is significant with respect to the total error on the test set. It all depends on the problem, we set a ceiling of how bad it is.
    For example, a 5% mismatch in a 10% error on test is better than a 50% mismatch on a 10% error.
### We were talking of cat detector, we can work on different approachs to solve the mismatch:
* Fix the dogs being recognized as cats
* Fix great cats from being misrecognized
* Improve performance on blurry images
* Categories of mistakes in general

Something Andrew recommends a spreadsheet for these approachs, using data from the dev set:

| Image       | Fix Dogs | Fix great cats   | Blurry        |Comments        |
| ----------- | ----------- | -----------   | -----------   |-----------   |
| 1           |   [x]       |               |               | Pug             |
| 2           |             | [x]           |               | Lince              |
| 3           |             |               | [x]           | Low quality          |
| ...         |             |               |               |              |
| Total       |    60%      |  15 %         | 5%            |5%            |

where 'Total' is the percentage of misrecognized images in that categories.
We might find new categories while searching through the images.
 
### We could have incorrectly labeled examples! 
* DL Algo are robust to random errors in the training set, for example, random mislabeled pics. 
* Systematic errors are a problem, it makes sense as a systematic error can be picked up by the algorithm and applied to real data outside the ML Loop. Crossfire
* We can add a new column to the previous table for incorrectly labeled.
* If it makes a significant difference to the dev test, take your time to fix mislabeled data. Checking against other error categories and the total error of the dev test, even after improving with different error cat.
* Remember that the dev test hels to select between two classifiers, if the dev set mislabeled data is significant, it can induce an error in this decision.
* Test and dev should be from the same distribution if possible.
* Changing dev/test mislabeled data can change the distribution as well.

###  Build your first system quickly, then iterate
* At the beginning, there are some many focus/directions to choose. What to pick to start? 
    * Set dev/test and metric
    * Build initial system, then use bias/variance analysis to prioritize next steps.
    * Don't make the first draft too complicated, don't be afraid to make it simple. It's a baby ML algo.

### Training and testing on different distributions (remember dev is validation)
* For examples, two sources of data (or more), these are different distributions.
* We could mix all sources together and shuffle the data: Pro - Train/Test/Dev same distribution. Con: the biggest dataset dominates the Test/dev split by the random shuffle. This option is not recommended.
* Another option, choose the biggest dataset as training set and split the smaller ones into test/dev. Maybe one dataset is more relevant than the others.
* What distributions are relevant to the problem? They are important to the dev/test splitting.
* Test/Dev splits can be way more smaller than what you think. More than 70k is a lot.
* What about bias and variance analysis? 
    * Keep a training dev set: A dev set of the same distribution as the training set to compare, so you might end up with: Train, Dev, Training-Dev and Test. The error from the Training-dev should be use a reference and we should optimize only on the dev set while training.

    ![Beautiful](/media/posts/diff_distribution.png)
    This is a great overview. Thank you Andrew.

* What about addressing data mismatch between Train and Dev?
    * Where are the differences? Can I artificially add it to the train? Be careful as adding the same information to the train might lead to overfitting this difference. Remember that ML is smarter than you and it will pick up any relevant pattern you add.


* Comments on transfer learning: You use it when you have really small dataset for training, therefore the dev/test set should be bigger than usual. The pretrain network needs less training data that a empty NN, so we can put them to work for us as dev/test instead.


* Multi-task Learning: 
    * It's just logistic regression for different outputs. This works nicely is the different tasks/labels have similar features in early layers (this are low-level features).
    * Labeling usually is more lazy or confusing.
    * Every task doesn't need to have the same amount of examples, this could be an issue for splitting data.
    * Usually bigger networks are needed.
    * An example of this is YOLO.

* Deep Learning:
    * Do you have A LOT of data?
    * Is the hand-design very complex and LOTS of data?
    * Hand-design could be very helpful, but choosing the wrong approach could severe the efficency of the DL network.
    * *Key question: Do you have sufficient data to learn a function of the complexity to map x to y?*
    * Nomenclature: End-to-End means that the model learns all the steps between the initiall input phase to the output result.

    



## Course 4: CNNs

