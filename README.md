# MechaCar_Statistical_Analysis
Statistical analysis of production data for AutosRUs' prototype vehicle the MechaCar.

## Linear Regression to Predict MPG

<p align="center">
<img src="https://github.com/mehill37/MechaCar_Statistical_Analysis/blob/82429a5eaf5772f59425806c708f3dd7af77c4ff/images/summaryregression.png">
</p><br/>

### Which variables/coefficients provided a non-random amount of variance to the mpg values in the dataset? 
- Some variables provide non-random amount of variance to the MPG values in our dataset.

Using multiple linear regression, and loading all variables into the model using the MechaCars dataset, we find that the ground_clearance, vehicle_length, and Intercept all have a significant impact on MPG. 

Each ```Pr(>ltl)``` value in the summary output represents the probability that the coefficient contributes a random amount of variance to the linear model. According to the results pictured above, we see the following statistically significant p-values, providing a non-random amount of variance to the mpg values:

- (Intercept) 5.08e-08
- vehicle-length 2.60e-12
- ground_clearance 5.21e-08

Because these values are so low (p<0.0001 in all cases), we can conclude that both vehicle length and ground clearance likely influence MPG.  

### Is the slope of the linear model considered to be zero?
- The slope of the linear model is not zero

Ground clearance and vehicle length variables were found and are statistically significant in predicting the response variable (MPG), so there is a non-zero slope.  

```MPG = 6.27(vehicle_length) + 0.001(vehicle_weight) + 0.07(spoiler_angle) + 3.55(ground_clearance) - 0.01```

### Does this linear model predict mpg of MechaCar prototypes effectively? 
- Further study is warranted to predict the MPG

Because Intercept is significant, there may be more variables contributing to the variations in MPG that are not included in this model. Therefore, this model will not predict MPG of MechaCar prototypes effectively until the other variables which contribute to the variations in MPG can be observed.

## Summary Statistics on Suspension Coils

The manufacturering team is asking the following question: 

    * The design specifications for the MechaCar suspension coils dictate that the variance of the suspension coils must not exceed 100 pounds per square inch. Does the current manufacturing data meet this design specification for all manufacturing lots in total and each lot individually? 

To provide the data the summarize() function is used to create a table of summary statistics on the PSI column in the Coils dataset for all of the lots. 

```
total_summary <- summarize(Coils, meanPSI=mean(PSI), medianPSI=median(PSI), variancePSI=var(PSI), SDPSI=sd(PSI))
```

<p align="center">
<img src="https://github.com/mehill37/MechaCar_Statistical_Analysis/blob/82429a5eaf5772f59425806c708f3dd7af77c4ff/images/total_summary.png">
</p><br/>

The variance of suspension coils for all manufacturing lots in total is 62.29 lbs/sq.in. . This meets the design specifications and does not exceed 100 lbs./sq.in. .

The data is then grouped by Manufacturing Lot to summarize the statistics for PSI within each lot. 

```
lot_grouping <- group_by(Coils, Manufacturing_Lot)

lot_summary <- summarize(lot_grouping, Mean=mean(PSI), Median=median(PSI), Variance=var(PSI), SD=sd(PSI))
```

<p align="center">
<img src="https://github.com/mehill37/MechaCar_Statistical_Analysis/blob/82429a5eaf5772f59425806c708f3dd7af77c4ff/images/lot_summary.png">
</p><br/>

By breaking down the statistics for each lot, we can see that in Lot 3, there is a variance in PSI of 170.29 lbs/sq.in. . This exceeds 100 PSI and no longer meets specifications.

## T-tests on Suspension Coils

The question of whether PSI across all manufacturing lots is statistically different from the population mean of 1,500 PSI is answered with the following code:

<p align="center">
<img src="https://github.com/mehill37/MechaCar_Statistical_Analysis/blob/82429a5eaf5772f59425806c708f3dd7af77c4ff/images/t_test.png">
</p><br/>

Here, we can see the results showing that the p-value = 1, which means that the mean of the PSI across all lots is not statistically different from the population mean of PSI of 1,500. We fail to reject the null hypothesis.

Now, we will run similar t-tests for each lot to compare PSI with the mean population PSI of 1,500.

Lot 1:
<p align="center">
<img src="https://github.com/mehill37/MechaCar_Statistical_Analysis/blob/82429a5eaf5772f59425806c708f3dd7af77c4ff/images/t_test_Lot1.png">
</p><br/>
We fail to reject the null hypothesis, because the P-value is less than 0.0001. 

Lot 2: 
<p align="center">
<img src="https://github.com/mehill37/MechaCar_Statistical_Analysis/blob/82429a5eaf5772f59425806c708f3dd7af77c4ff/images/t_test_Lot2.png">
</p><br/>
We fail to reject the null hypothesis, because the p-value is 0.0006.

Lot 3: 
<p align="center">
<img src="https://github.com/mehill37/MechaCar_Statistical_Analysis/blob/82429a5eaf5772f59425806c708f3dd7af77c4ff/images/t_test_Lot3.png">
</p><br/>
For Lot 3 we reject the null hypothesis, because the p-value is 0.1589. This means that the PSI values on Lot 3 could as much be a result of chance as any other factor measured.

## Study Design: MechaCar vs Competition

