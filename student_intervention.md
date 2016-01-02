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

### 3. Preparing the data

The provided code was used to map the features from categorical
data to numerical data.

The data was split into 300 training examples and 95 test examples.
The pandas routine 'sample' was used to randomly select from the
student data. If random sampling is not done, then if the student
data was order will all the passing students first and then all
the failing students, the test set would be all failing students
and no meaningful testing could be done.  While such an ording is
and extreme case, some other bias could be present in the ording
of the data, so random selection is necessary.

If the just predict 'pass' for all students was run agaist the test
set.
  * precision 0.74
  * recall    1.00
  * F1        0.85

### 4. Training and Evaluation Models

From the possible scikit-learm learning model, Decision Tree,
Nearest Neighbor, and Support Vector Machine classifier were
chosen.

Decision Tree (DT) was chosen because it has the best potential for
generating an easily understandable model.  Decision Tree are also
less distorted by outliers since the values of the features are not
involved in some compuation where an extreme value throws off a
calcuation such as mean.  They are fast and scaleable.  The downside
is they often overfit.  Using a Random Forest of decision trees can
often deal with the overfitting, but that also reduces the
'understandablity' of the end model.

Support Vector Machines (SVM) are known for generating highly
accurate models.  Thru the use of the 'C' parameter, which 
controls the amount of acceptable errors, SVM can be steered
clear of overfitting.  The downside is that SVM also have
a lot of parameters to play with and one can become obsessed
with playing with all the parmaeters to get the last bit of
accuracy.  They suffer most of the chosen algorithms for use
of computer resouces (including runtime).

Nearest Neighbors (NN), like Decision Trees, benefit from an ease
of explanation of the process.  NN are simple, flexible, and able
to be incrementally improved while running (just add new data
points). NN can also use very little computation resources to train.
The downside is the computational resources are used when it comes
time to predict.  The "nearest", part, while intuitively appealing,
can turn out to be difficult to define and require a lot of time
picking the right parameters.  The computation of the distance
metric and turn out to be computationally expensive.


```
| model | Train | Train  | Predict | Train | Test |
|       | size  | time   | time    | F1    | F1   |
| DT    |  300  | 0.003  | 0.000   | 1.00  | 0.76 |
| DT    |  200  | 0.001  | 0.000   | 1.00  | 0.78 |
| DT    |  100  | 0.001  | 0.000   | 1.00  | 0.69 |
```
Fast runtime. Train time decrease with sample size.
'Perfect' fit to training. Train results not good 
match with Test. Decrease in F1 as lowest sample
size.

```
| model | Train | Train  | Predict | Train | Test |
|       | size  | time   | time    | F1    | F1   |
| NN    |  300  | 0.002  | 0.008   | 0.86  | 0.78 |
| NN    |  200  | 0.001  | 0.005   | 0.81  | 0.81 |
| NN    |  100  | 0.001  | 0.002   | 0.82  | 0.76 |
```
Slow runtime. Train time decrease with sample size.
Better match of results from Train to Test. Relatively
consistent results as sample size decreases.

```
| model | Train | Train  | Predict | Train | Test |
|       | size  | time   | time    | F1    | F1   |
| SVM   |  300  | 0.007  | 0.006   | 0.86  | 0.85 |
| SVM   |  200  | 0.004  | 0.004   | 0.85  | 0.84 |
| SVM   |  100  | 0.002  | 0.001   | 0.86  | 0.86 |
```

Relativel Slow training and runtime. Decrease of 
train set size neglibible effect on train and test
F1 scores while resulting in lower train and predict
time.

### 5. Choosing the Best Model

#### Choice of model

I selected to purse the SVM model.  It had the highest F1 score on
all three trainset sizes
  * 300:  0.85 vs  0.76, 0.78
  * 200:  0.84 vs  0.78, 0.81
  * 100:  0.86 vs  0.69, 0.76

In terms of time efficency both the SVM and NN were comperable, both much
worse that DT.  The results for the SVM suggest it did not suffer from 
limiting the training set to a subset an available data as the F1 score 
for 300,200,and 100 hundred were within 0.01 of 0.85.  I believe that
the SVM training set size could be selected to fit the compuational 
resource budget.  In other words the budget would be the driver.

Realalistically the computatinal budget on this project should be
dwarfed by other cost of the project. The largest school district
in the country has less than 1,000,000 students [1].  In the 1990s
I was able to build SVM classifier on datasets with >10 times as
many records with >100 times as many features in less than a day
on low end consumer PCs.  Figure out a budget of time, if the full
dataset doesn't train, select a random sample of the 1/2^n graduating
senior (100,000 students at most) if need to reduce time, and run
on a laptop. Repeat, lowering n, until you are under time budget.

#### How the model is suppose to work

The model works by taking the existing data and attempting to 
divide it into two classes based on the 'passed' label.  As a
simplification, imagine instead of 31 features, that there were
only two.  Each student would be plotted on a graph on a sheet of
paper.  Then one would look for the line that divided the 'yes'es
from the 'no's.  The line would be chosen to both divide the two
groups and to create a boundry on each side of the line that was
farthest from all the closest points.  The computer is doing a 
similar thing but is capable of working in much higher dimentions
and capable of adding new dimensions to make the split with the
N-dimensional equivalent of a line, a hyperplane.

My recommendation to the board of supervisors would be to build a
SVM model with the currently available data.  The model would be
used to identify students that are predicted to not pass.  The 
model can do this with 83% (5/6) accuracy.  The model has 20%
recall, so most students who are going to fail will not be identified.
Given the limited resourse of the group, this isn't necessarily
a big problem.  The limited resource can be used to intervene with 
the small group of students very likely to fail this academic year.  

Part of the budget should be used to collect data to allow better
models to be build.  A specific recommendation would be to collect
a score on the final exam, so a prediction of the score instead of
just pass fail would be possible.  It might be a better strategy
to identify students closest to passing, which would benefit most
effectively from an intervention.

#### Final F1 Score

The final F1 Score for the predition of passing student was 0.86.
Recall that the F1 score for ignoring input and just predicting
'pass' for each student on the same test set was 0.85.

#### Addendum

While asked to maximize the F1 score, in the end I think it is
important to concentrate on the confusion matrix.  In this case the
SVM was able to construct a highly precise predictor of students
that would not pass.  The recall was pretty bad, but giving a
situation of limited resources, one can choose to intervene with a
limited number of student.  and bring the graduation rates up with
a more focused approach instead of spreading resource across more
student.

I attempted to build classifier with better recall, but doing so
dramatically increased the false preditions of failing the exam.
One would have to decide how to interpret devoting resouces to
student that would likely pass anyways.  Might not be a bad thing,
as there overall eduation might be improved, but it would likely
be seen as a mis spending of money since not aligned with the goal
of increaing graduation rate.  Ultimately, test score data, as
opposed to pass/fail data, might be better at identifying student
who with a bit of intervention can more from fail to pass.  data


[1] (2010 largest school districts in the US) [https://en.wikipedia.org/wiki/List_of_the_largest_school_districts_in_the_United_States_by_enrollment]
