# FinalProject_3340
Final Project for Math3340 on Real estate data
Model fitting
Use Library leaps to perform all subsets regression

data=read.csv("~/Downloads/Real estate.csv")
> data=as.matrix(data[,-1])
leaps(x=data[,-1],y=data[,1],method="adjr2")
Largest R^2 adjusted is [17]=>0.0311625915
should be [38] this would give us the correct model T T T T T F
According to the adjusted R^2 Criterion, the model chosen is the one with the largest adjusted R^2,
in this case, this is the model with second Row of 4> T T F F F T
This is the model X1,X2,X6 

Is the model satisfactory?
> y=data[,7]; x1=data[,1];x2=data[,2];x3=data[,3];x4=data[,4];x5=data[,5];x6=data[,6]
newmodel=lm(y~x1+x2+x4+x5+x6)
esresids=rstudent(newmodel)
par(mfrow=c(2,1))
> qqnorm(esresids,main="normal QQ plot of externally standardized residuals")
plot(fitted(newmodel),esresids,xlab="fitted values",ylab="ext stand resids",main="externally standardized residuals vs fitted values")


Now stepwise Procedure:
read.csv("~/Downloads/Real estate.csv")
nullmodel=lm(y~1)
fullmodel=(lm(y~x1+x2+x3+x4+x5+x6))
step1=step(nullmodel,scope=list(lower=nullmodel,upper=fullmodel),direction="forward")
summary(step1)
we get:
model
y ~ x3 + x4 + x2 + x5 + x1


fullmodel2=lm(y~x1*x2*x1*x3*x1*x4*x1*x5*x1*x6*x2*x3*x2*x4*x2*x5*x2*x6*x3*x4*x3*x5*x3*x6*x4*x5*x4*x6*x5*x6)
step2=step(fullmodel2,direction="backward")
summary(step2)

anova(step1,step2) => 
  we get
  Model 1: y ~ x3 + x4 + x2 + x5 + x1
 Model 2: y ~ x1 + x2 + x3 + x4 + x5 + x6 + x1:x3 + x2:x3 + x1:x4 + x2:x4 + 
  x3:x4 + x2:x5 + x3:x5 + x4:x5 + x2:x6 + x3:x6 + x4:x6 + x1:x3:x4 + 
  x2:x3:x4 + x2:x3:x5 + x2:x4:x5 + x2:x3:x6 + x2:x4:x6 + x3:x4:x6 + 
  x2:x3:x4:x6

step(nullmodel,scope=list(lower=nullmodel,upper=fullmodel2),direction="both")
lm(formula = y ~ x3 + x4 + x2 + x5 + x1 + x3:x4 + x3:x5 + x4:x5 + 
     x3:x4:x5)
Backwardmodel2=lm(formula = y ~ x3 + x4 + x2 + x5 + x1 + x3:x4 + x3:x5 + x4:x5 + 
                   x3:x4:x5)
Backwardmodel1=lm(formula=y ~ x3 + x4 + x2 + x5 + x1)
library(car)
vif(Backwardmodel1) =  
  x3       x4       x2       x5       x1 
2.016593 1.611395 1.013325 1.584992 1.013918 

vif(Backwardmodel2)
x3           x4           x2           x5           x1 
8.058634e+06 1.438626e+07 1.028153e+00 1.101398e+01 1.019818e+00 
x3:x4        x3:x5        x4:x5     x3:x4:x5 
7.364742e+06 8.052063e+06 1.439052e+07 7.364468e+06 






