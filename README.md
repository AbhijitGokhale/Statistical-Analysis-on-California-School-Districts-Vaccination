# Statistical-Analysis-on-California-School-Districts-Vaccination
The project explains specific and appropriate statistical values; both frequentist and Bayesian inferential evidence; explanation including both data exploration and cleaning and appropriate diagnostics.

## Introduction & Objective
Goal for this project is to conduct the necessary analyses of vaccination rates in California school districts and then write up a technical report for a scientifically knowledgeable staff member in a California state legislator’s office. There should be sufficient numeric and graphical detail that the staff member can create a comprehensive briefing for a legislator.

The project explains specific and appropriate statistical values; both frequentist and Bayesian inferential evidence; explanation including both data exploration and cleaning and appropriate diagnostics.

## Dataset
* RData file contains two data sets that pertain to vaccinations for the U.S. as a whole and for Californian school districts. The U.S. vaccine data is a time series, and the California data is a sample of end-of-year vaccination reports from n=700 school districts.

* **usVaccines:** Time series data from the World Health Organization reporting vaccination rates in the U.S. for five common vaccines
(Note: DTP1 = First dose of Diphtheria/Pertussis/Tetanus vaccine (i.e., DTP); HepB_BD = Hepatitis B, Birth Dose (HepB); Pol3 = Polio third dose (Polio); Hib3 – Influenza third dose; MCV1 = Measles first dose (included in MMR))

* **districts:** A sample of California public school districts from the 2017 data collection, along with specific numbers and percentages for each district:

**Feature Dictionary**
- DistrictName    : Name of the district
- WithDTP         : Percentage of students in the district with the DTP vaccine
- WithPolio       : Percentage of students in the district with the Polio vaccine
- WithMMR         : Percentage of students in the district with the MMR vaccine
- WithHepB        : Percentage of students in the district with Hepatitis B vaccine
- PctUpToDate     : Percentage of students with completely up-to-date vaccines
- DistrictComplete: Boolean showing whether or not district’s reporting was complete
- PctBeliefExempt : Percentage of all enrolled students with belief exceptions
- PctMedicalExempt: Percentage of all enrolled students with medical exceptions
- PctChildPoverty : Percentage of children in district living below the poverty line
- PctFamilyPoverty: Percentage of families in district living below the poverty line
- PctFreeMeal     : Percentage of students in the district receiving free or reduced cost meals
- Enrolled        : Total number of enrolled students in the district
- TotalSchools    : Total number of different schools in the district

* As might be expected, the data are quite skewed: districts range from 1 to 582 schools enrolling from 10 to more than 50,000 students. Further, while most districts have low rates of missing vaccinations, a handful are quite high. 

## Implementation
* Univariate & Bivariate Data Exploration
* Correlation Analysis, Outlier Analysis, Data Transformations (log, sqrt, cbrt, etc.)
* Time series analysis to understand trends in vaccination rates - Autocorrelation Function(acf), Process of Whitening, Augmented Dicky Fuller Test(ADF test )
* Descriptive and Inferrential Statistics
* **Linear Regression:**
    * A linear regression was performed to estimate the percentage of all enrolled students with completely up-to-date vaccines with use of interaction between PctChildPoverty and Enrolled_log. We decided to center the data to get the better interaction results between two predictors.
    * We decided to interpret the interaction term first, in case it influences how we make sense out of the linear main effects. In this case the interaction PctChildPoverty_cntr*Enrolled_log_cntr coefficient is statistically not significantly different from 0 with a t-value of -1.485 and a p-value greater than 0.05 and we failed to reject the null hypothesis.
    * Bi-variate exploratory data analysis done earlier made us use the data which was log transformed for analysis, which generally improved the skew and the linearity of the relationship. The main linear effect found strong support for the relationship (F(3,692)=35.32, p-value<0.001, adjusted R2 = 0.129). Among predictors, PctChildPoverty_cntr (b=0.22740, t=6.055, p<0.001) and Enrolled_log_cntr (b=2.41176, t=8.557, p<0.001) were significant.
    * A Bayesian regression also found overwhelming evidence in support of a model with significant predictors PctChildPoverty and Enrolled_log. The BayesFactor analysis shows that Bayes Factor of 1.270309e+18:1 are very strong odds in the favor of alternative hypothesis that a interaction model is better than intercept model. So we reject the null hypothesis which suggest that Intercept only model is better. The sampled coefficients had similar values, a mean of 0.222966 for PctChildPoverty_cntr with an 95% HDI of 0.15019 to 0.29506, and a mean of 2.361761 for Enrolled_log_cntr with an 95% HDI of 1.81599 to 2.92110. 
    * Apart from this, we can see that, a mean of -0.037283 for an interaction PctChildPoverty_cntr.&.Enrolled_log_cntr with 95% HDI of -0.08596 to 0.01264 shows that HDI has 0, which tells us that interaction is not a good predictor because there is chance that mean value is 0. This result is perfectly aligning with the traditional linear model analysis.
    * Overall, we can say that interaction between PctChildPoverty and Enrolled_log is not significant to estimate of the percentage of all enrolled students with with completely up-to-date vaccines , but still interaction model’s main linear effect will be able to predict the percentage of all enrolled students with with completely up-to-date vaccines correctly.

* **Logistic Regression:** 
    * A logistic regression was performed on data to test how Percentage of children in district living below the poverty line(PctChildPoverty), Percentage of families in district living below the poverty line(PctFamilyPoverty), Total number of enrolled students in the district(Enrolled) and Total number of different schools in the district(TotalSchools) predict whether or not district’s reporting was complete(DistrictComplete), dichotomized.
    * As explained earlier, the distributions were highly skewed for Enrolled and TotalSchools, so the data were log transformed for analysis, which generally improved the skew and the linearity of the relationship. The variables with percentage values were not transformed to not to hamper the data meaning and its overall effect on the dependent variable.
    * In addition to this, after getting normal odds of TotalSchools_log, we converted the log transformation back to TotalSchools to gather the exact normal odds and 95% CI of Total number of different schools in the district.
    * The results showed a significant association of both PctFamilyPoverty (b=-0.06760, Z(693)=-3.445, p<0.001) and TotalSchools_log (b=-0.76661, Z(693)=-5.343, p<0.01). In regular odds, each unit increase in Percentage of families in district living below the poverty line changes the odds of the district’s reporting to be complete by 0.9346332; each unit increase in the TotalSchools increases the odds 1.591 times. The 95% confidence intervals were 0.899 to 0.972 for PctFamilyPoverty and 1.41414 to 1.840958 for TotalSchools.
    * The model showed poor performance with a Tjur’s pseudo-R2 of 0.081 and but shows an accuracy of 94.54%.A Bayesian analysis reached similar conclusions, though the log odds of sampled coefficients differed slightly: a mean of -0.06687 for PctFamilyPoverty with an HDI of -0.1059 to -0.02581 and -0.78787 for TotalSchool_log with an HDI of -1.0887 to -0.50268. Neither HDI contains 0, suggesting that these variables are predictive. 
    * In summary, the higher the Percentage of families in district living below the poverty line and Total number of different schools in the district, the greater the chance of the district’s reporting being completed.

* BayesFactor determination along with Marcov Chain Monte Carlo simulation to identify 95 % high density interval analysis

## Conclusion and Recommendations
- In the analysis we are trying to understand which factors are affecting to predict Percentage of all enrolled students with belief exceptions, percentage of students with completely up-to-date vaccines and whether or not district’s reporting was complete.

- Among all the regression analysis, Frequentist approach and Baysian approches are coinciding with each other. So we can conclude and suggest some recommendations with strong confidence.

- The above analysis shows us that if there are students with one vaccine, there is high chance that students likely to have all of the others vaccines because of the high correlation within Tetanus, Polio, MMR and Hepatitis B. With this result in mind we can setup a system to get all the 4 vaccinations reporting done at all vaccination places.

- Furthermore, we need to allocate financial resources by investing into charity drives or aid drives to the reduce the percentage of families in district living below the poverty line. Also we can direct some financial help to the schools in the districts by introducing free meals drives or free education drives about importance of having vaccines. This can be linked to a new system that after done with vaccinations incentives such as coupons, will be given to the helpers assisting government official in reporting. These strategies would help in getting reporting done where we have large number of students, greater area to cover and large number of schools.

- Also we need to have some kind of interaction between total number of enrolled students in the district and percentage of children in district living below the poverty line. The interaction would help for more in depth understanding to allocate financial resources accurately to the districts and which would essentially help us to get more vaccinations and reporting done.

- The drives for enrolled students mentioned above will also help to improve percentage of students with completely up-to-date vaccines. There is very less information available on percentage of all enrolled students with belief exceptions. But we can say from the correlation matrix that this is highly negatively correlated with percentage of students with completely up-to-date vaccines. We can study this thoroughly and provide  some more understanding on improving the overall vaccination rates if more information is available to us. The availability of Hib3 and MCV1 vaccines rates for all Californian districts and the availability of MMR vaccine rates all over the US could have also shed some insights in understandning the  into understanding and improving vaccination and reporting rates.
