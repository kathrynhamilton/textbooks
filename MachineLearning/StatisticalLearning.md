# An Introduction to Statistical Learning

James, Witten, Hastie, Tibshirani

Kathryn Hamilton - March 2018

## 1 - Introduction

Statistical learning is a set of tools for modeling and understanding complex datasets. These tools can be classified as **supervised** or **unsupervised**.

* **Supervised** learning predicts an output based on one or more inputs. Examples include linear regression and logistic regression.

* **Unsupervised** learning has inputs and no supervised output, but can still be used to learn relationships and structure. The primary example of this is cluster analysis.

------

Three example datasets are used throughout this book:

* `Wage` - Income information for males in the central Atlantic region of the United States from 2003 to 2009. The goal is to predict income based on education, age, and year (Regression).
* `Smarket` - Daily return information of the S&P stock index from 2001 to 2005. The goal is to predict whether the market will increase or decrease on a given day (Classification).
* `NCI60` - Gene expression data for 64 cancer cell lines. The goal is to determine whether there are groups or clusters among the cell lines based on their expression measurements (Clustering).

There are **R** libraries and the above datasets available on the book's [website](http:/www.StatLearning.com) to work through the book's examples and labs.

## 2 - Statistical Learning

### What is Statistical Learning?

For input variables $X_1, X_2, \dots , X_p$ and output response $Y$ we assume that there is some relationship $Y=f(X)+\epsilon$, where $\epsilon$ is a zero-mean random error term independent of $X$. *Statistical learning is a set of approaches to estimate $f$.* We call this estimate $\hat{f}$.

The accuracy of $\hat{f}$ depends on both **reducible error** and **irreducible error**. This book focuses on methods of reducing reducible error.

* **Reducible error** is introduced when $\hat{f}$ is not a perfect estimate for $f$.  
* **Irreducible error** is the result of unmeasured variables that are useful in predicting $Y$ and any other unmeasurable variation.

------

There are two motivations to estimate $f$: **prediction** and **inference**.

In situations where $X$ is readily available but $Y$ is not, we can **predict** $Y$ using an estimate of $f$: $\hat{Y} = \hat(f)(X)$. In general, $\hat{f}$ is not a perfect estimate for $f$ because it cannot predict the irreducible error $\epsilon$. Here we can treat $\hat{f}$ as a black box.

In other situations, we are interested in understanding the way that $Y$ is affected as $X$ changes. This is called **inference**. We still need to estimate $f$ but cannot treat $\hat{f}$ as a black box as we are interested in understanding the relationship between $X$ and $Y$ as opposed to predicting $Y$. We may want to know:  

* Which predictors are most strongly associated to the response?
* What is the relationship between the response and each predictors?
* Which relationships can be summarized using a linear equation? Which are more complicated?

*Many problems fall into both of these categories.* For example, consider an advertising firm that would like to know which form of media advertising generates the largest boost in sales (inference), and how much of an increase in sales would occur given an advertising increase in that specific media (prediction).

*The best method for estimating $f$ depends on the goal and what you are trying to achieve.*

------

Most statistical learning methods can be classified as either **parametric** or **non-parametric**.

**Parametric methods** first make an assumption about the form of $f$, which typical involves some parameters, and then uses training data to fit the model and thus provide estimate values for each parameter. Assuming a parametric form simplifies the problem of estimating $f$, but can be dangerous if the model chosen does not represent the data sufficiently well or is overly complicated.

**Non-parametric methods** do not make an explicit assumption about the form of $f$. They seek an estimate of $f$ by getting as close to the data as possible while limiting noise and overfitting. The advantage is that they can be fit accuractely to a wide range of possible shapes, thus avoiding the possibility of poor fit. However, solving these types of problems are can be very difficult and the results are often not easy to interpret.

------

Various statistical methods have a trade off between **interpretability** and **flexibility**. Inference problems favor restrictive models with higher interpretability. Prediction problems favor more flexible models as they are more likely to be accurate (at the risk of overfitting) and thus provide better predictions. Some exemplary methods are as follows:

* **Subset Selection** and **Lasso** have high interpretability and have low flexibility.
* **Bagging**, **Boosting** and **Support Vector Machines** have high flexibility and low interpretability.
* **Least Squares**, **Generalized Additive Models** and **Trees** have moderate flexibility and moderate interpretability.

------

Variables in a statistical learning problem are either **quantitative** or **qualitative** (categorical). We tend to refer to problems with a quantitative response as **regression** problems while those involving a qualitative response are referred to as **classification** problems.

### Assessing Model Accuracy

*There is no free lunch* in statistics: no one method dominates all others over all possible datasets. Hence, it is an important task to decide which method produces the best results for the particular dataset at hand.

To measure how well predictions match observed data we use the following error functions, where $y_i$ is the observed value and $\hat{f}(x_i)$ is the predicted value of the response:

* **Mean Squared Error** (MSE) for regression problems, $MSE=\frac{1}{n} \sum_{i=1}^{n}(y_i-\hat{f}(x_i))^2$.
* **Error Rate** for classification problems, $\text{Error rate}=\frac{1}{n}\sum_{i=1}^{n} I_{(y_i)}\neq \hat{f(x_i)}$.

Models with smaller error predict more accurately that those with larger error.

These accuracy metrics are meant to be performed on *unseen data that has not been used to fit the model*, known as the test set. In practice, computing the test error can be very difficult as response data is not usually available. Sometimes the training error can approximate the test error. Otherwise, **cross-validation** or **partitioning** must be used to estimate the test error using the training data.

------

In order to minimize expected test error, the chosen statistical method *must simulatenously acheive* **low variance** *and* **low bias** where:

* **Variance** is the amount by which $\hat{f}$ would change if the model were fitted using a different training set.
* **Bias** is the error that is introduced by approximating a real-life problem with a simplified model.

------

Test error rate is minimized, on average, by a classifier that *assigns each observation to the most likely class*.

The **Bayes Classifier** for quantitative responses operates under this premise, by predicting the class of $x_0$ to be $j$ when $P(Y=j \, | \, X=x_0) is the greatest out of all possible classes.

The **Bayes error rate** is $1-E\left(\max_j P(Y=j \, | \, X)\right)$, which is analogous to the irreducible error.

**K-Nearest Neighbors** (KNN) follows the same theory for qualitative responses. However, conditional probability can only be estimated rather than calculated directly so this method is weaker than the Bayes Classifier. 

KNN identifies the K closest observations to $x_0$, called $N_0$. It then estimates the conditional probability for class $j$ as the ratio of neighbouring responses in that class, $P(Y=j \, | \, X=x_0) \approx \frac{1}{K}\sum_{i\in N_0}I_{(y_i=j)}$, and predicts the class of $x_0$ in the same manner as Bayes.

*The choice of $K$ is very important.* As $K$ grows the model becomes less flexible. The optimal $K$ value is often neither small nor large, but somewhere in the middle.

## 3 - Linear Regression

### Simple Linear Regression

We assume a linear relationship between a quantitative response Y and a single predictor variable X: $Y \approx \beta_0+\beta_1X$.

When we regress $Y$ on $X$ we obtain estimates ($\hat{\beta_0}$, \, $\hat{\beta_1}$) for ($\beta_0$, \, $\beta_1$) such that the model fits as close as possible to the available data, $Y = \hat{Y} + \epsilon = \hat{\beta_0}+\hat{\beta_0}X + \epsilon$.

The most common was to do this is by least squares regression, which minimizes the residual sum of squares (RSS). This gives:

\begin{aligned}
\hat{\beta_1} &= \frac{\sum_i=1^n (x_i-\bar{x})(y_i-\bar{y})}{\sum_i=1^n (x_i-\bar{x})^2} \\
\hat{\beta_0} &= \bar{y}-\hat{\beta_1}\hat{x} \\
RSS &= \sum_i 1^n e_i = \sum_i 1^n (y_i-\hat{y_i})
\end{aligned}

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
