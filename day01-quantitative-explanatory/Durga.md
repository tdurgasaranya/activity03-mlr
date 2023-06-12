---
## Durga Tummalapalli
title: "Activity 3 - MLR"
output: activity_Durga.Rmd
---
- Find the knit document for my work on Rstudio here:
[knit document](https://rstudio.gvsu.edu/s/1a9bab708b7b83241e6c5/file_show?path=%2Ftmp%2FRtmpVNPnXv%2Fpreview-11d3932893a3fd.html)

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

##loading the required libraries and checking for the packages

```{r}
library(tidyverse)
library(tidymodels)

library("GGally")

```

### Loading a dataset and creating the Data frame

```{r}
df <- read.csv("https://raw.githubusercontent.com/stedy/Machine-Learning-with-R-datasets/master/insurance.csv")

df

head(df)

```
- Dimensions of the dataset 1338 rows and 7 columns

### Creating a univariate graph using two type of plots
### Type 1

- This helps to understand the statistics and outliers of the dataset within this dataframe


```{r}

boxplot(df$bmi)

```
### Type 2
- Barplot explains the frequency distribution of categorical variable
- Density plot is used for a continous valued variables


```{r}

barplot(table(df$bmi))
plot(density(df$bmi))


```

### Understanding 
- univariate graphs are helpful in understanding all the characteristics of the variables like tendency, variability and outliers.

### checking relationship between two variables with univariate graph analysis


```{r}
boxplot(df$charges)
```



```{r}

barplot(table(df$charges))
plot(density(df$age))


```
- While checking for relationship between two variables whether there is an overlap, no two variables seem to have overlapping factor to determine relationships.

### two other quantitative variables to describe the patterns in the response variable.

- From the statistical point of view when checking for relationships between two quantitative variables it helps to determine the relationship and characteristics of two variables is
- Predictive modeling
- Exploratory data analysis
- Decision making would be effective if the relationship is determined between two variables

```{r}
library(GGally)

#variables in scatter plot matrix
variables <- c("bmi", "charges")

#scatterplot matrix
ggpairs(df[, variables])


```

```{r}
library(GGally)

df %>%
  select(age, bmi) %>%
  ggpairs()

```

- The correlation value 0.198 indicates that there is a weak linearity relationship between the two variables used here Charges and bmi.
- So if one value increase relatively there is increase in second value.

```{r}
library(GGally)

df %>%
  select(age, charges) %>%
  ggpairs()
```
- here the two variables are not strongly linear to determine any prediction modelling

### Multi Regression model


```{r}
lm_spec <- linear_reg() %>%
set_mode("regression") %>%
set_engine("lm")

lm_spec

mlr_mod <- lm_spec %>% 
fit(charges ~ bmi + bmi, data = df)

tidy(mlr_mod)
```

## Fit the multiple linear regression model

```{r}


model <- lm(bmi ~ age + bmi + charges, data = df)

# coefficients
coefficients <- coef(model)

cat("y =", coefficients[1], "+", coefficients[2], "* x1 +", coefficients[3], "* x2 +", coefficients[4], "* x3")


```
### 3D PLOTS:
- 3D plots can be created using scatter3D functions and this is not very interactive visual in Github rather it appears as a steady graph
- Although it provides a clear depiction of clustering of datasets groups it is not good with Git as the limitations to represent all the dimension visualization
-  GGally::ggpairs  displays the output as images on Git and is very understandable from Git

```{r}

library(plot3D)

data <- df

# Create a 3D scatter plot
scatter3D(data$bmi, data$charges, data$age, pch = 16, col = "blue",
          xlab = "X", ylab = "Y", zlab = "Z", main = "3D Scatter Plot")


```
