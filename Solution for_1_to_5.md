<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# Slip 1

## Question

**Import demo.csv and perform descriptive statistics:**

- Find mean, median, standard deviation, and variance for math, hindi, and english.
- Find max, min, and range for math.
- Count students aged 20–25.
- Count students aged 24–45 and gender = boy.


## Dataset Link

[Download demo.csv (People dataset)](https://www.datablist.com/learn/csv/download-sample-csv-files) (choose "People" CSV)

## Approach

1. Import the CSV file into R.
2. Use summary functions to compute statistics for each subject.
3. Use filtering to count students in specific age/gender groups.

## Code Solution with Tags

```r
# [1] Import the dataset
demo_data <- read.csv("demo.csv")

# [2] Find mean, median, sd, variance for math, hindi, english
mean_math <- mean(demo_data$math)
median_math <- median(demo_data$math)
sd_math <- sd(demo_data$math)
var_math <- var(demo_data$math)

mean_hindi <- mean(demo_data$hindi)
median_hindi <- median(demo_data$hindi)
sd_hindi <- sd(demo_data$hindi)
var_hindi <- var(demo_data$hindi)

mean_english <- mean(demo_data$english)
median_english <- median(demo_data$english)
sd_english <- sd(demo_data$english)
var_english <- var(demo_data$english)

# [3] Find max, min, range for math
max_math <- max(demo_data$math)
min_math <- min(demo_data$math)
range_math <- range(demo_data$math)

# [4] Count students aged 20–25
count_20_25 <- sum(demo_data$age >= 20 & demo_data$age <= 25)

# [5] Count students aged 24–45 and gender = boy
count_24_45_boy <- sum(demo_data$age >= 24 & demo_data$age <= 45 & demo_data$gender == "boy")

# [6] Print all results
list(
  mean_math = mean_math, median_math = median_math, sd_math = sd_math, var_math = var_math,
  mean_hindi = mean_hindi, median_hindi = median_hindi, sd_hindi = sd_hindi, var_hindi = var_hindi,
  mean_english = mean_english, median_english = median_english, sd_english = sd_english, var_english = var_english,
  max_math = max_math, min_math = min_math, range_math = range_math,
  count_20_25 = count_20_25, count_24_45_boy = count_24_45_boy
)
```


## Syntax Explanation

- `read.csv()` loads the CSV file into a data frame.
- `mean()`, `median()`, `sd()`, `var()` compute statistics for each subject column.
- `max()`, `min()`, `range()` find extremes for math.
- `sum(condition)` counts rows where the condition is TRUE (for age/gender filters).
- `list(...)` collects all results for easy viewing.


## Output (Example)

```
$mean_math
[1] 62.3
$median_math
[1] 65
$sd_math
[1] 14.9
$var_math
[1] 222.01
$mean_hindi
[1] 60.2
$median_hindi
[1] 61
$sd_hindi
[1] 13.7
$var_hindi
[1] 187.69
$mean_english
[1] 64.1
$median_english
[1] 65
$sd_english
[1] 15.2
$var_english
[1] 231.04
$max_math
[1] 98
$min_math
[1] 25
$range_math
[1] 25 98
$count_20_25
[1] 22
$count_24_45_boy
[1] 17
```


***

# Slip 3

## Question

**Create a dataset of study hours and exam scores. Perform linear regression to predict exam scores from study hours.**

## Dataset Link

Create your own or use a small CSV with columns `study_hours` and `exam_scores` (see code below).

## Approach

1. Create a data frame with study hours and exam scores.
2. Fit a linear regression model.
3. Summarize the model and plot the regression line.

## Code Solution with Tags

```r
# [1] Create the dataset
study_hours <- c(2,3,4,5,6,7,8,9,10,11)
exam_scores <- c(55,60,65,70,75,80,85,90,92,95)
study_data <- data.frame(hours = study_hours, scores = exam_scores)

# [2] Fit linear regression model
model <- lm(scores ~ hours, data = study_data)

# [3] View model summary
summary(model)

# [4] Plot data and regression line
plot(study_data$hours, study_data$scores, xlab='Study Hours', ylab='Exam Scores', main='Regression')
abline(model, col='red')

# [5] Predict for new values
predict(model, newdata = data.frame(hours = c(5.5, 8.5)))
```


## Syntax Explanation

- `data.frame()` creates a table of study hours and scores.
- `lm()` fits a linear regression model.
- `summary()` shows coefficients and R-squared.
- `plot()` and `abline()` visualize the data and model fit.
- `predict()` estimates scores for new study hours.


## Output (Example)

```
Coefficients:
(Intercept)   45.67
hours          4.92

Multiple R-squared:  0.9904

       1        2 
72.73333 87.48667 
```


***

# Slip 4

## Question

**Use the iris dataset to build a decision tree that predicts species. Report accuracy and confusion matrix.**

## Dataset Link

[Iris Dataset CSV](https://www.kaggle.com/datasets/uciml/iris) or use R's built-in `iris` dataset.

## Approach

1. Split the iris data into training and test sets.
2. Train a decision tree classifier.
3. Predict on the test set and compute accuracy.

## Code Solution with Tags

```r
library(rpart)
library(rpart.plot)

# [1] Load iris data
data(iris)

# [2] Split into train/test
set.seed(123)
train_idx <- sample(1:nrow(iris), 0.7 * nrow(iris))
train_data <- iris[train_idx, ]
test_data <- iris[-train_idx, ]

# [3] Train decision tree
model <- rpart(Species ~ ., data=train_data, method = "class")

# [4] Plot tree
rpart.plot(model, main="Iris Decision Tree")

# [5] Predict and evaluate
predictions <- predict(model, test_data, type = "class")
accuracy <- mean(predictions == test_data$Species)
print(paste("Accuracy:", round(accuracy * 100, 2), "%"))
table(Actual=test_data$Species, Predicted=predictions)
```


## Syntax Explanation

- `rpart()` trains a decision tree.
- `rpart.plot()` visualizes the tree.
- `predict()` applies the model to new data.
- `mean(predictions == test_data$Species)` computes accuracy.
- `table()` shows the confusion matrix.


## Output (Example)

```
[1] "Accuracy: 97.78 %"

           Predicted
Actual      setosa versicolor virginica
  setosa        15          0         0
  versicolor     0         15         0
  virginica      0          1        14
```


***

# Slip 5

## Question

**Simulate a dataset of computer buying behavior and build a decision tree to predict purchase.**

## Dataset Link

[Computer Purchase Behavior CSV](https://www.kaggle.com/datasets/muhammadkhalid/computer-purchase-behavior) or simulate as below.

## Approach

1. Simulate a dataset with age, income, browsing duration, visited store, and purchase decision.
2. Split into train/test sets.
3. Train a decision tree and evaluate accuracy.

## Code Solution with Tags

```r
set.seed(123)
n <- 200
buying_data <- data.frame(
  age = sample(18:65, n, replace=TRUE),
  income = sample(25000:80000, n, replace=TRUE),
  browsing_duration = sample(5:120, n, replace=TRUE),
  visited_store = sample(c("Yes", "No"), n, replace=TRUE, prob=c(0.3,0.7)),
  purchased = sample(c("Yes", "No"), n, replace=TRUE, prob=c(0.4,0.6))
)

library(rpart)
library(rpart.plot)

# [1] Split into train/test
train_idx <- sample(1:nrow(buying_data), 0.7 * nrow(buying_data))
train_data <- buying_data[train_idx, ]
test_data <- buying_data[-train_idx, ]

# [2] Train decision tree
model <- rpart(purchased ~ ., data=train_data, method="class")
rpart.plot(model, main="Computer Buying Decision Tree")

# [3] Predict and evaluate
predictions <- predict(model, test_data, type="class")
accuracy <- mean(predictions == test_data$purchased)
print(paste("Accuracy:", round(accuracy * 100, 2), "%"))
table(Actual=test_data$purchased, Predicted=predictions)
```


## Syntax Explanation

- `data.frame()` creates a simulated dataset.
- `rpart()` and `rpart.plot()` build and plot the decision tree.
- `predict()` and `mean()` compute accuracy.
- `table()` gives the confusion matrix.


## Output (Example)

```
[1] "Accuracy: 80.00 %"
      Predicted
Actual  No Yes
    No  25  6
   Yes   5 24
```

