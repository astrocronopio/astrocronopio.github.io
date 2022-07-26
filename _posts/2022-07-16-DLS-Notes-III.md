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
    * Improve performanace on blurry images
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

### Training and testing on different distributions
    * For examples, two sources of data (or more)
    * We could mix all sources together and shuffle the data: Pro - Train/Test/Dev same distribution. Con: the biggest dataset dominates the Test/dev split by the random shuffle. This option is not recommended.
    * Another option, choose the biggest dataset as training set and split the smaller ones into test/dev. Maybe one dataset is more relevant than the others.


    



## Course 4: CNNs

