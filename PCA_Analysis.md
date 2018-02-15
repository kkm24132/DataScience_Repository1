---
title: "PCA_Analysis"
author: "Kamal"
date: "February 15, 2018"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```


```{r cars}
## Principal Component Analysis in R

install.packages("scatterplot3d")
library(scatterplot3d)

# Retrieve the "iris" dataset, sans the "Species" column.
iris_numerical <- iris[,-5]

scatterplot3d(iris[,1:3],xlab = "Sepal Length",ylab="Sepal Width",zlab="Petal Length")

# Perform PCA on the numerical data from "iris"
# prcomp does all the work of centering and scaling our data for us!
pcaSolution <- prcomp(iris_numerical,center = TRUE,scale. = TRUE)

# Print a summary of the analysis
print(pcaSolution)
summary(pcaSolution)

plot(pcaSolution, type="l", main="Eigenvalues for each Principal Component")

# Considering that the data has been centered and scaled, the mean of the eigenvalues should be equal to one.
# Calculate and print the eigenvalues for the principal components.
# The eigenvalues are calculated by squaring the standard deviation values for each component.
eigenvalues <- (pcaSolution$sdev)**2
eigenvalues
{
  # Plot the Scree plot.
  screePlot <- plot(pcaSolution, type="l", main="Eigenvalues with Kaiser-Guttman cutoff")
  
  # Add a cutoff line based on the mean of the eigenvalues.
  # This should be equal to one for centered and scaled data.
  abline(h=mean(eigenvalues),lty=2,col="red")
}

# Retrieve the values of the observations for each principal component.
rotated_values <- pcaSolution$x

# Print out the first six rows of data.
head(rotated_values)

# Visualizing the two components..
dim(rotated_values)
rotated_values = as.data.frame(rotated_values)
colors = iris[,5];
levels(colors)= c(1,2,3)
plot(rotated_values$PC1, rotated_values$PC2, xlab="Principal component 1",
     ylab="principal component 2", pch = 20, cex=2,
     col=adjustcolor(colors,alpha.f=0.5))
legend(2,2, legend=levels(iris[,5]),pch=20,cex=0.8,col=levels(colors))


```
