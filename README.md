# R-code-
`insurance.(1)` <- read.csv("D:/insurance (1).csv")
View(`insurance.(1)`)

head(`insurance.(1)`)
str(`insurance.(1)`)
plot(`insurance.(1)`)

#Splitting test and training data
set.seed(2)
library(caTools)
split <- sample.split(`insurance.(1)`,SplitRatio = 0.6)
split
train <- subset(`insurance.(1)`,split="TRUE")
test <- subset(`insurance.(1)`,split="FALSE")
train
test

#Making a lm model on the following data
model <- lm(charges~ age+sex+bmi+children+smoker+region , data=train)
summary(model)
#Prediction
model <- lm(charges~ age+bmi+children+smoker, data=train)
pred <- predict(model,test)
pred
#Comparison
plot(test$charges, type = 'l', lty= '96', col = "red")
lines( pred , type = "l", col = "yellow" )
plot(pred, type = 'l', lty= '96', col = "yellow")        
rmse<- sqrt(mean(pred- train$charges)^2)
rmse
rmse<- sqrt(mean(pred- test$charges)^2)
rmse
