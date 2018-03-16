# An Introduction to Statistical Learning with Applications in R

James, Witten, Hastie, Tibshirani
Kathryn Hamilton - March 2018

## 1 - Introduction

Statistical learning is a set of tools for modeling and understanding complex datasets. These tools can be classified as **supervised** or **unsupervised**.

Supervised learning predicts an output based on one or more inputs. Unsupervised learning has inputs and no supervised output, but can still be used to learn relationships and structure.

Three example datasets are used throughout this book:

* `Wage` - Income information for males in the central Atlantic region of the United States from 2003 to 2009. The goal is to predict income based on education, age, and year (Regression).
* `Smarket` - Daily return information of the S&P stock index from 2001 to 2005. The goal is to predict whether the market will increase or decrease on a given day (Classification).
* `NCI60` - Gene expression data for 64 cancer cell lines. The goal is to determine whether there are groups or clusters among the cell lines based on their expression measurements (Clustering).

There are **R** libraries and datasets available to work through the book's examples and labs on the book's [website](http:/www.StatLearning.com).

## 2 - Statistical Learning

### What is Statistical Learning?

For input variables $X_1, X_2, \dots , X_p$ and output response $Y$ we assume that there is some relationship $Y=f(X)+\epsilon$, where $\epsilon$ is a zero-mean random error term independent of $X$. Statistical learning is a set of approaches to estimate $f$.

There are two reasons to estimate $f$: prediction and inference.

In situations where $X$ is readily available but $Y$ is not, we can **predict** $Y$ using an estimate of $f$: $\hat{Y} = \hat(f)(X)$. In general, $\hat{f}$ is not a perfect estimate for $f$ because it cannot predict the irreducible error $\epsilon$. Here we can treat $\hat{f}$ as a black box.

In other situations, we are interested in understanding the way that $Y$ is affected as $X$ changes. This is called **inference**. We still need to estimate $f$ but cannot treat $\hat{f}$ as a black box as we are interested in understanding the relationship between $X$ and $Y$ as opposed to predicting $Y$. We may want to know:

* Which predictors are most strongly associated to the response?
* What is the relationship between the response and each predictors?
* Which relationships can be summarized using a linear equation? Which are more complicated?

Many problems fall into both of these categories. For example, consider an advertising firm that would like to know which form of media advertising generates the largest boost in sales (inference), and how much of an increase in sales would occur given an advertising increase in that specific media (prediction). The best method for estimating $f$ depends on the goal and what you are trying to achieve.

### Assessing Model Accuracy

## 3 - Linear Regression

### Simple Linear Regression
### Multiple Linear Regression
### Other Consideration in the Regression Model
### The Marketing Plan
### Comparison of Linear Regression with K-Nearest Neighbors

## 4 - Classification

### An Overview of Classification
### Why Not Linear Regression?
### Logistic Regression
### Linear Discriminant Analysis
### A Comparison of Classification Methods

## 5 - Resampling Methods

### Cross-Validation
### The Bootstrap

## 6 - Linear Model Selection and Regularization

### Subset Selection
### Shrinkage Methods
### Dimension Reduction Methods
### Considerations in High Dimensions

## 7 - Moving Beyond Linearity

### Polynomial Regression
### Step Functions
### Basis Functions
### Regression Splines
### Smoothing Splines
### Local Regression
### Generalized Additive Models

## 8 - Tree-Based Methods

### The Basics of Decision Trees
### Bagging, Random Forests, Boosting

## 9 - Support Vector Machines

### Maximal Margin Classifier
### Support Vector Classifiers
### Support Vector Machines
### SVMs with More than Two Classes
### Relationship to Logistic Regression

## 10 - Unsupervised Learning

### The Challenge of Unsupervised Learning
### Principal Components Analysis
### Clustering Methods
