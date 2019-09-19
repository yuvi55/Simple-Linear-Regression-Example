# Simple-Linear-Regression-Example
Simple Linear Regression Performed on a Test Data Set with Graph
#SIMPLE LINEAR REGRESSION


#import data set

dataset = read.csv('Salary_Data.csv')
#dataset = dataset[,2:3]

#Creating a training and a test dataset

#install.packages('caTools')

library(caTools)
set.seed(123)
split = sample.split(dataset$Salary,SplitRatio = 2/3) # We take $Purchased because it is the dependant variable
training_set = subset(dataset , split == TRUE)
test_set = subset(dataset , split == FALSE)

# Factoring the values for calculation

#training_set[ ,2:3] = scale(training_set[ ,2:3])
#test_set[ ,2:3] = scale(test_set[ ,2:3])

# Regression

regressor = lm(formula = Salary ~ YearsExperience, data = training_set)

#Predicting what salaries should be

y_predict = predict(regressor, newdata = test_set)

# Graph plotting

#install.packages('ggplot2')

  # Training set

library(ggplot2)

ggplot() +
  geom_point(aes(x = training_set$YearsExperience,y = training_set$Salary),
             colour = 'blue') +
  geom_line(aes(x = training_set$YearsExperience, y = predict(regressor, newdata = training_set)),
             colour = 'red') +
  ggtitle('Salary vs Experience (Training set)') +
  xlab('Years of experience') +
  ylab('Salary')

# Test Set
ggplot() +
  geom_point(aes(x = test_set$YearsExperience,y = test_set$Salary),
             colour = 'blue') +
  geom_line(aes(x = test_set$YearsExperience, y = predict(regressor, newdata = test_set)),
            colour = 'red') +
  ggtitle('Salary vs Experience (Test set)') +
  xlab('Years of experience') +
  ylab('Salary')


