# survival-analysis
kaplan-meier survival curve and COX model based risk-adjusted surviavl curve

#load the required R package
#library(survival)
#library(survminer)
#library(ggsci)
#read your data 
#mydata<-read.csv("C:/Users/Desktop/data.csv",header = T,sep = ",")
#head(mydata)
#fit.cox<-survfit(Surv(time, status) ~ age_group, data = mydata)
ggsurv <- ggsurvplot(fit.cox, 
                     pval=T,
                     data=mydata,
                     conf.int = TRUE,
                     risk.table = TRUE,
                     ggtheme = theme_bw())
