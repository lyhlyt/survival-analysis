# survival-analysis
kaplan-meier survival curve and COX model based risk-adjusted surviavl curve

#load the required R package
library(survival)
library(survminer)
library(ggsci)

#read your data 
mydata<-read.csv("C:/Users/Desktop/data.csv",header = T,sep = ",")
head(mydata)

#factor variables 
mydata$age_group<- factor(mydata$age_group, levels=c(1,2,3), 
                          labels=c("A","B","C"))
mydata$edu_group <- factor(mydata$edu_group, levels=c(1,2,3), 
                           labels=c("A1","B1","C1"))
mydata$marital_group <- factor(mydata$marital_group, levels=c(1,2,3), 
                               labels=c("A2","B2","C2"))

#set the reference subgroup
relevel(mydata$age_group,ref=1)
relevel(mydata$edu_group,ref=1)
relevel(mydata$marital_group ,ref=1)

#formula
S<-Surv(time_year, status)~age_group+edu_group+marital_group

#fit COX regression model
f<-coxph(S,data = mydata)
summary(f)

#generate forest map
ggforest(f,fontsize=0.8, cpositions = c(0.02,0.14, 0.4),noDigits=2)

#export the forest map as a vectorgraph to a PPT file
library(export)
graph2ppt(file="Fig.10.pptx", width=8, height=6)

 ############

#plot risk-adjusted survival curve
ggadjustedcurves(f,
                 data=mydata,
                  xlim=c(1,2,3,4,5),
                  variable="haha",
                  palette = "jco",
                  xlab="xlab",
                  ylab = "ylab",
                  legend.title="main",
                  legend.labs=c("a","b","c","d"),
                  legend = "bottom",
                  ggtheme = theme_survminer())
