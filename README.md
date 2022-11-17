# Paycheck Protection Program Impacts on Food Service Business Closure Rates in Oregon
## An Analysis of PPP Forgiveness Ratio as a Predictor for Food Service Business COVID Survival Rate
Economic and political science pundits predicted massive permanent business closures as the first wave of state and federal COVID mandates struck businesses in early 2020. Particularly affected by the COVID crisis were businesses operating in the retail and food service sectors, and many projections put restaurants and food service business closure rates at 75%. A federal program was developed to curtail long-term damage to the economy, aimed at providing relief to businesses by supplementing cash flow for specific burdensome operating costs; payroll, rent and utilities. The Paycheck Protection Program (PPP) was a massive dispersal of federal loan funds to businesses throughout 2020 and 2021, with the added potential to have loan debt forgiven if certain need-based criteria were met. This analysis will focus specifically on the impact of loan dispersal and loan forgiveness on business closure rates. More specifically the analysis will determine if 4 main elements of the PPP loan are predictors for business closure status for the Food Service Sector in Oregon; Initial Loan Amount, Loan Forgiveness Ratio, Loan Approval Date and Jobs Reported. A machine learning model will identify the 2 elements that are the most significant predictors of whether a business remained open or closed permanently. Ultimately the analysis will provide insight into whether the PPP program was effective at reducing the number of business closures due to COVID.


## Oregon PPP Statistical Analysis Snapshot
### Comparative Study PPP Loan Dispersal by Industry in Oregon
A snapshot analysis of PPP funding to the state of Oregon provides a comparative study of funding across all business sectors. This comparison highlights statistics of mean loan size, mean forgiveness rate, total loan value and other aspects recorded by the PPP funding office for each loan recipient across business industries.

![Screen Shot 2022-11-14 at 10 23 56 PM](https://user-images.githubusercontent.com/107326987/202343153-c49ee2f5-be1f-4b8a-8a02-675025f060ad.png)
![Screen Shot 2022-11-14 at 10 23 41 PM](https://user-images.githubusercontent.com/107326987/202342849-83193ec4-a700-4892-85bb-c29d3f5e06c3.png)
![Screen Shot 2022-11-15 at 7 02 19 PM](https://user-images.githubusercontent.com/107326987/202342887-527c6120-6572-4f40-954e-1c00e505cacc.png)

- Food establishments made up 9.9% of loan recipient count, but received only 9.7% of distributed funds.
-	The average loan size for food service establishment was $114,141, $2,785 less than the average loan value for non-food establishments.
-	The average forgiveness ratio for food establishments is 93.7%, 1.4% less than non-food establishment forgiveness ratio.
- Geographic distribution of funds clusters follows population density with largest amounts of funds distributed around Portland, Salem, Eugene and Bend city centers.

## Oregon Food Service Sector: PPP Program Impact on Business Closure Rates
### This granular analysis will look at 4 elements of the PPP loans for each food service business that received funding; loan value, forgiveness ratio, reported jobs, loan dispersal/approval date. This incisive analysis will provide the basis for the building and execution of a machine learning model that will prove/disprove the hypothesis that reported jobs and forgiveness ratio are the most significant predictors for closure rates.

Data Sourcing : The PPP data was secured from the Small Business Association governmental website, the SBA was the entity that received applications and distributed funds. The SBA PPP data provided datapoints on Loan Amount, Approval Date and Jobs Reported. Forgiveness Ratio was a data point added by performing a function on the original PPP data. The data was filtered for the State of Oregon and further filtered by industry. The PPP loan recipients were assigned federally categorized 7 digit NAICS codes based on the industry type provided by applicant. The data was filtered for all business with an NAICS code starting with 722 – all business identified as food service including but not limited to restaurants, grocery stores, bakeries. 

In order to explore the relationship between these data points and closure rates, our original dataset was merged with data secured from Yelp. A Yelp API call was designed to return an exhaustive list of Oregon food establishments using 13 key search terms (i.e restaurant, bakery, deli, grocery etc) that would overlap completely with establishments covered under the selected NAICS umbrella. The returned json dataset from the API call was converted to a dataframe and merged  with the PPP data on Oregon Food service loan recipients on the common data point of Address. The assumption was made that on a left join, using the PPP Oregon Food Service dataframe as the left dataframe, anywhere the two dataframes matched was a business that was still open. A second merge was performed with all active business registry data on mailing address from the State of Oregon Corporation Division. Below is an illustration of the relationships between each raw data source.

![Screen Shot 2022-10-19 at 8 42 53 PM](https://user-images.githubusercontent.com/107326987/202343241-b7376ab8-b45e-49e6-bc11-7b82dea1ba1c.png)

The final merged dataframe was used to produce visualizations exploring the relationships between our 4 identified loan elements and business closure status.

![Screen Shot 2022-11-14 at 10 24 14 PM](https://user-images.githubusercontent.com/107326987/202343078-47cfec6d-8a0a-4a03-bffe-748877902883.png)
- 53% of PPP loan recipients ultimately closed, and 47% remained open through the end of Q3 2022. The average forgiveness ratio for closed business is 92.98%, the average forgiveness ratio for business that remained open is 94.38%. The forgiveness ratio for open businesses is 1.4% higher than for closed businesses.
![Screen Shot 2022-11-14 at 10 24 49 PM](https://user-images.githubusercontent.com/107326987/202343144-49a8d796-8012-4595-8cba-891647808260.png)
- The incidence of business closures increases and surpasses the count of open business around April of 2021. Loan recipients who received funding or were approved before April 2021 had a higher likelihood of remaining open, that outcome dramatically flip-flopped after April of 2021.

## Supervised Machine Learning : Forgiveness Ratio and Approval Date as predictors for Closure Status
### Hypothesis : Forgiveness Ratio and Business Size (measured by reported jobs) are the biggest predicotrs in determing business status: a larger forgiveness ratio and larger job count will lead to a higher likelihood of a business remaining open.

A classification machine learning model using logistic regression was used to predict business closure status based on the 4 loan elements identified earlier - Forgiveness Ratio, Jobs Reported, Loan Amount, Approval Date (ranked hierarchically in assumed significance). 
![Screen Shot 2022-11-14 at 10 31 38 PM](https://user-images.githubusercontent.com/107326987/202343200-c7ff841d-ec30-4ce9-9d1e-7244ed229c25.png)
- The model has a 62% accuracy score at predicting the classification 0 (closed businesses) and a slightly smaller accuracy score of 55% at predicting for the classifier 1 (open business).

![Screen Shot 2022-11-14 at 10 31 47 PM](https://user-images.githubusercontent.com/107326987/202343205-d33d56ee-a293-44ae-a3c1-0d76581b7359.png)
- Approval Date is the mos significant measured loan predictor for closure status. We can see that born out in our visualization earlier that showcased April 2021 as the threshold for businesses being more or less likely to remain open. 
- Forgiveness ration was the 2nd strongest indicator for closure status, which is also born out in our visualizations.
- Reported Jobs was the weakest predictor for classification. Whether a company employed 500 or 5 employees was less significant than when a business recieved their funding. 

## Final Analysis : Natural "Churn" Rate in Food Service Sector & PPP Impact on Closures
### Pre-COVID Food Industry "Churn" Rate vs Churn Rate of PPP Recipients
The closure rate of food service business pre-COVID, otherwise known as the industry "churn" rate is 30% annually. With 53% of business receiving funding closing over 2 years, this shows an average closure rate of 26% over each year, 4% below the average churn rate. (source Washington Post). This is signifact reduction considering that not only did COVID closures exceed the economically stabilized churn rate of 30, but was less. Where you might assume the churn/closure rate would increase to 35 or 40% during COVID, dropped to 26%.  This is the measured impact of COVID closure. So PPP funding had impact on closure rate compared to food service industry business that did not receive funding. The strongest predictor was Approval Date, so business that were able to receive funding in the first round, and most importantly before DATE/DATE were most likely to remain open. 

### Assumptions in Data Profile
Below are the limitations of and assumptions made on the data provided. 
- The Yelp data was gathered using an API call for all zipcodes for 13 different identified key search terms (i.e restaurant, bakery, deli, grocery etc). The first assumption is that the key serach terms used int he API call would overlap completely with the terminology and business sectors covered in the chosen NAICS code. Despite documentation in the Yelp API call, it did not return any closed business and could not be used as a dataset to determine a comparative analysis of closure reates between business that did and did not receive funding.
- All business matched during the merge. However businesses can change address. All 
- Business will often have several names; a legal name and a dba ('doing business as') name. Often business are nested inside of other business. The business name was note an element of each datapoint that would provide an overlap for merging our PPP provided government data and our Yelp API data. The data was merged on the address provided. Here the assumption is that PPP business remained at the address provided on the loan application. Business provided their "principal place of business" address on the PPP loan application rather than the address associated with an LLC office or home address of a managing officer.

## Data Sources
Yelp Food Service Data - https://www.yelp.com/developers/documentation/v3/get_started

PPP Loan Data - https://www.sba.gov/funding-programs/loans/covid-19-relief-options/paycheck-protection-program/ppp-data

Oregon Business Active Registries - https://data.oregon.gov/

https://www.washingtonpost.com/food/2022/06/21/covid-restaurant-closures/

https://pos.toasttab.com/blog/on-the-line/restaurant-failure-rate

![Screen Shot 2022-10-31 at 8 55 44 PM](https://user-images.githubusercontent.com/107326987/202554917-928d88a5-bcf1-46f1-81e5-2002940a40fc.png)

