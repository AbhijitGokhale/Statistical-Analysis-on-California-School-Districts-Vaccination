# Statistical-Analysis-on-California-School-Districts-Vaccination

## Objective
The goal is to conduct the necessary analyses of vaccination rates in California school districts and then present a technical report for a scientifically knowledgeable staff member in a California state legislator’s office. The technical report should be of sufficient numeric and graphical detail that the staff member can create a comprehensive briefing for a legislator (see question 10 for specific points of interest). The staff member understands the concept of statistical significance and other basic concepts like mean, standard deviation, and correlation. 

The report should be clear, concise, with explanation of specific and appropriate statistical values; inclusion of both frequentist and Bayesian inferential evidence (i.e., it is not sufficient to just examine the data); explanation of any included tabular material and the appropriate use of graphical displays when/if necessary. It is also important to conduct a thorough analysis, including both data exploration and cleaning and appropriate diagnostics. Bonus points will be awarded for work that goes above expectations.

Make sure to include enough statistical information so that another analytics professional could review your work. Your report can include graphics created by R, keeping in mind that if you do include a graphic, you will have to provide some accompanying narrative text to explain what it is doing in your report. 

## Feature Dictionary
DistrictName    : Name of the district
WithDTP         : Percentage of students in the district with the DTP vaccine
WithPolio       : Percentage of students in the district with the Polio vaccine
WithMMR         : Percentage of students in the district with the MMR vaccine
WithHepB        : Percentage of students in the district with Hepatitis B vaccine
PctUpToDate     : Percentage of students with completely up-to-date vaccines
DistrictComplete: Boolean showing whether or not district’s reporting was complete
PctBeliefExempt : Percentage of all enrolled students with belief exceptions
PctMedicalExempt: Percentage of all enrolled students with medical exceptions
PctChildPoverty : Percentage of children in district living below the poverty line
PctFamilyPoverty: Percentage of families in district living below the poverty line
PctFreeMeal     : Percentage of students in the district receiving free or reduced cost meals
Enrolled        : Total number of enrolled students in the district
TotalSchools    : Total number of different schools in the district

## Implementation
Time series analysis to understand trends in vaccination rates
Regression analysis along with interaction among certain features

## Conclusion and Recommendations
- In the analysis we are trying to understand which factors are affecting to predict Percentage of all enrolled students with belief exceptions, percentage of students with completely up-to-date vaccines and whether or not district’s reporting was complete.

- Among all the regression analysis, Frequentist approach and Baysian approches are coinciding with each other. So we can conclude and suggest some recommendations with strong confidence.

- The above analysis shows us that if there are students with one vaccine, there is high chance that students likely to have all of the others vaccines because of the high correlation within Tetanus, Polio, MMR and Hepatitis B. With this result in mind we can setup a system to get all the 4 vaccinations reporting done at all vaccination places.

- Furthermore, we need to allocate financial resources by investing into charity drives or aid drives to the reduce the percentage of families in district living below the poverty line. Also we can direct some financial help to the schools in the districts by introducing free meals drives or free education drives about importance of having vaccines. This can be linked to a new system that after done with vaccinations incentives such as coupons, will be given to the helpers assisting government official in reporting. These strategies would help in getting reporting done where we have large number of students, greater area to cover and large number of schools.

- Also we need to have some kind of interaction between total number of enrolled students in the district and percentage of children in district living below the poverty line. The interaction would help for more in depth understanding to allocate financial resources accurately to the districts and which would essentially help us to get more vaccinations and reporting done.

- The drives for enrolled students mentioned above will also help to improve percentage of students with completely up-to-date vaccines. There is very less information available on percentage of all enrolled students with belief exceptions. But we can say from the correlation matrix that this is highly negatively correlated with percentage of students with completely up-to-date vaccines. We can study this thoroughly and provide  some more understanding on improving the overall vaccination rates if more information is available to us. The availability of Hib3 and MCV1 vaccines rates for all Californian districts and the availability of MMR vaccine rates all over the US could have also shed some insights in understandning the  into understanding and improving vaccination and reporting rates.
