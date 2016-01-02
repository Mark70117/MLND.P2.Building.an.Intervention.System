# P2: Building an Interventino System // Udacity Machine Learning Nanodegree
### Mark Anderson
 * [github](https://github.com/Mark70117)
 * [linkedin](https://www.linkedin.com/in/mark-anderson-4b702718)

## Synopsis

The goal of this project is to model the factors that predict how
likely a student is to pass their high school final exam. An number
of classifier were constructed.  Classifiers were build using
Decision Tree, Nearest Neighbor,and Support Vector Machines. The models
were evaluated on a number of dimension: 1) their F1 score, 2) the size
of the training set, and 3) computation resources.

## Editorial Comments

The winner, by the three factors the model is suppose to be evaluated
on, is the "Just say 'pass'" classifier.  On the complete data set,
just saying every student will pass has a F1 score of 0.80.  The
recall of the "Just say 'pass'" classifier is 100% on identifying
passing students, and the precision is 0.67.  Even worse, thru the
luck of random select, on the test set select the F1 score is 0.85.
The model taks no computer training time, no computer prediction
time, in fact no computational resources whatsoever.  There seems
to be some miscommunication (perhaps mine) in this process.  If the
the title is correct, and intervention is the goal, then predicting
"pass" (the explicitly stated objective), which a large majority
of the students do, it not a good objective.

## Questions and Report Stucture

### 1. Classification vs Regression

The feature we are attempting to predict from the data set is
'passed'.  The 'passed' feature takes on the values 'yes' and 'no'.
So given this categorical type of the data a classification system 
better matches.  Personally, as a responsible software engineer, I
would push back to the client to see if there is perhaps a test
score available, which for the purpose of identifying students that
might benefit from intervention would be preferable.  In addition
to identifying students that could fail, it could help identify
borderline students who passed becuase of random luck on the final
exam.

### 2. Exploring the data

The following describes the shape of the dataset.
  * Total number of students: 395
  * Number of students who passed: 265
  * Number of students who failed: 130
  * Number of features: 31
  * Graduation rate of the class: 67.09%

To get a baseline of what how effective our eventual model is over
basically doing nothing, I also evaluated the data versus the "Just
say 'passed'" as a predictive model.  The prediction of that model
ignores all the input features and just outputs "passed"
  * Just say yes precision: 0.67
  * Just say yes recall: 1.00
  * Just say yes F1: 0.80


