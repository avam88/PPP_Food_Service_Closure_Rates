# COVID Restaurant Closures & PPP Loan Forgiveness Analysis
## Project Overview
### Economic and political science pundits predicted massive permanent business closures as the first wave of state and federal COVID mandates struck businesses in early 2020. Particularly affected by the COVID crisis were businesses operating in the retail and food service sectors, and many projections put restaurants and food service business closure rates at 75%. A federal program was developed to curtail long-term damage to the economy, aimed at providing relief to business by supplementing cash flow for specific predominant operating costs; payroll, rent and utilities. The Paycheck Protection Program (PPP) was a massive dispersal of federal loan funds to business throughout 2020 and 2021, with the added potential to have loan debt forgiven if certain need-based criteria were met. This analysis will focus specifically on the long-term impact of loan dispersal and forgiveness on business status (whether a business remained open through the end of 2022 or permanently closed). In relation to closure rates for the Food Service Sector in Oregon this analysis we will be focusing on 4 elements; Initial Loan Amount, Loan Forgiveness Ratio, Loan Approval Date and Jobs Reported. Ultimately our machine learning model will determine if these 4 elements are predictors for business status.

Our hypotheses is that Forgiveness Ratio and Business Size (measured by reported jobs) are the biggest determining factors in business status: a larger forgiveness ratio and larger job count will lead to businesses with fewer closures. Ultimately our analysis will provide insight into whether the PPP program on a comprehensive level was effective at lessening business closures.

## Oregon PPP Statistical Analysis: Contextual Rundown
### A snapshot analysis of PPP funding to the state of Oregon will provide a comparative study of funding across all business sectors. There will be further exploration of funding and loan forgiveness statistics within the food service sector in Oregon. This granular analysis will look at 5 factors for each food service business that received PPP funding; loan value, forgiveness value, forgiveness ratio, reported jobs, loan dispersal/approval date. This incisive analysis will provide the basis for the building and execution of a machine learning model that will prove/disprove the hypothesis that the 5 factors explored for OR food service business loan recipients is a predictor for closure rates.

### Comparative PPP Loan Dispersal Analysis: Food Service Sector vs State Statistics
To provide context the machine learning model exploring loan dispersal elements as predictors for business survival, we will first provide a wide angle snapshot of the PPP funding program in Oregon. The comparison highlights statistics of mean loan size, mean forgiveness rate, total loan value and other aspects recorded by the PPP funding office for each loan recipient. 

Dataframe image here

-	Bullet points

## Oregon Food Service Sector PPP Impact on Business Closure Rates
### The PPP data was secured from the PPP governmental website. It provided datapoints on Loan Amount, Approval Date, Jobs Reported. Forgiveness Ratio was a data point added by performing a function on the original PPP data. The data was filtered for the State of Oregon and further filtered by industry. The PPP loan recipients were assigned federally categorized NAICS codes based on the industry type provided by applicant. The data was filtered for all business with an NAICS code starting with 722 – all business identified as food service including but not limited to restaurants, grocery stores, bakeries. In order to explore the relationship between these data points and closure rates, our original dataset was merged with data secured from Yelp. 

A yelp API call was designed to return an exhaustive list of Oregon food establishments using 13 key search terms (i.e restaurant, bakery, deli, grocery etc) that would overlap completely with the terminology and business sectors covered in the chosen NAICS code. The returned json dataset was converted to a dataframe and merged  with the PPP date on Oregon Food service loan recipients on the common data point of Address. The assumption was made that on a left join, using the PPP Oregon Food Service dataframe as the left dataframe, anywhere the two dataframes matched was a business that was still open. A second merge was performed to capture any business that are still open, but may have changed location, or temporarily closed a location, merge with Oregon State active business registry, mailing and primarily place of business address to capture more business. 

From this dataframe we used to produce our visualizations of the relationships between our 4 identified elements (loan amount, forgiveness ratio, approval date, jobs).

Images here
-	We can see that open business have a higher forgiveness rate
-	We can see that recipients of the loan in the first wave (months 1 – 3) had a higher incidence of being open, passed over the threshold of this date, and we can see the count of closed business out pace open.
-	Not a strong correlation between jobs and business status

## Supervised Machine Learning : Forgiveness Ratio and Approval Date as predictors for Closure Status

A classifier model using logistic regression. Based on the 4 elements of Forgiveness Ratio, Jobs, Loan Amount, Approval Date (ranked hierarchically in assumed significance), is a business open or closed. We can see that Approval Date has the greatest measured impact on closure status. We can see that born out in our visualization show that after DATE/DATE the closure rates swapped.

Jobs was the weakest predictor for classification. Whether a company employed 500 or 5 employees was less significant than approval date and forgiveness rate. 
Using Random Forrest Modeling, our machine learning model accuracy score.
Ranked elements in relative impact on closure rates.
We see that Approval Date and Forgiveness Rate have the most impact, are the strongest predictors. We see that play out in our vizualizations.


## Final Analysis : Natural "Churn" Rate in Food Service Sector & PPP Impact on Closures

### The closure rate of food service sector business pre-COVID, otherwise known as the industry "churn" rate is 30% annually. With 53% of business receiving funding closing over 2 years, this shows an average closure rate of 26% over each year, 4% below the average churn rate. (source Washington Post). This is signifact reduction considering that not only did COVID closures exceed the economically stabilized churn rate of 30, but was less. Where you might assume the churn/closure rate would increase to 35 or 40% during COVID, dropped to 26%.  This is the measured impact of COVID closure. So PPP funding had impact on closure rate compared to food service industry business that did not receive funding. The strongest predictor was Approval Date, so business that were able to receive funding in the first round, and most importantly before DATE/DATE were most likely to remain open. 


## Data Sources
Yelp
PPP
Oregon Business
https://www.washingtonpost.com/food/2022/06/21/covid-restaurant-closures/
https://pos.toasttab.com/blog/on-the-line/restaurant-failure-rate

### Assumptions in Data Profile
Below are the limitations of and assumptions made on the data provided. 
- The Yelp data was gathered using an API call for all zipcodes for 13 different identified key search terms (i.e restaurant, bakery, deli, grocery etc). The first assumption is that the key serach terms used int he API call would overlap completely with the terminology and business sectors covered in the chosen NAICS code. Despite documentation in the Yelp API call, it did not return any closed business and could not be used as a dataset to determine a comparative analysis of closure reates between business that did and did not receive funding.
- All business matched during the merge. However businesses can change address. All 
- Business will often have several names; a legal name and a dba ('doing business as') name. Often business are nested inside of other business. The business name was note an element of each datapoint that would provide an overlap for merging our PPP provided government data and our Yelp API data. The data was merged on the address provided. Here the assumption is that PPP business remained at the address provided on the loan application. Business provided their "principal place of business" address on the PPP loan application rather than the address associated with an LLC office or home address of a managing officer.
