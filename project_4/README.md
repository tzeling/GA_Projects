<img src="http://imgur.com/1ZcRyrc.png" style="float: left; margin: 20px; height: 55px">

# Project 4 - West Nile Virus Prediction

--- 

# Executive Summary

The West Nile Virus (WNV) is a mosquito-borne disease commonly transmitted to humans via the bite of an infected mosquito. The aim of this project was to build a model to predict where pesticides should be sprayed to effectively target WNV in the city of Chicago, Illinois. As part of the Disease And Treatment Agency, we were provided data of mosquito traps (with information on whether WNV was detected), data on pesticide spraying and data on weather conditions. Through exploratory data analysis of the data, we noted that various weather factors such as temperature, relative humidity and precipitation could affect the reproduction and survival rates of mosquitoes, increasing the prevalence of WNV. Analysis on time and seasonality showed that WNV season started in July and lasted till September with the peak in August. The spray dataset was used for data visualisation and showed that there was little change in the number of WNV mosquitoes after spraying - this may be attributed to ineffective spraying, where WNV high risk areas were not sprayed.

A total of 4 models were evaluated - (i) Logistic Regression; (ii) Support Vector Classifier; (iii) K-Nearest Neighbors (KNN); and (iv) Random Forest. The data was split into a training and testing dataset. Our target was to achieve an ROC AUC score as well as a recall score of at least 0.7, with Synthetic Minority Oversampling Technique (SMOTE) used in the modelling. Out of the 4 models, only Logistic Regression met the target. It had a testing ROC AUC score of 0.8, and a testing recall score of 0.75. KNN was our baseline model and it had a testing ROC AUC score of 0.75, and a testing recall score of 0.54. The low recall score means many false negatives were predicted by the KNN model, which is unfavourable.

A cost-benefit analysis was also done on the data. The costs analysed include the cost of the spraying of pesticides. The benefits analysed include the cost avoidance of medical and productivity costs from preventing cases of WNV through the spraying of pesticides in Chicago. The analysis found that the benefit-cost ratio would be >= 1 if we prevented 100 WNV cases. Spraying the whole of Chicago on a weekly basis was observed to be a costly and inefficient endeavour if undertaken. A more effective approach would be to target spraying at areas that have a high predicted probability of WNV outbreak.

The project found that presence of WNV was affected by time of year, with the mosquito season peaking in July to September. The three biggest weather indicators that affected the mosquito outbreak was temperature, humidity, and precipitation. Rain generally led to less mosquitoes in the short term, likely due to disturbance of stagnant water bodies. However, a spike in mosquitoes was also possible after the rain due to creation of new stagnant water bodies. It was discovered that past spray campaigns were poorly targeted and had limited impact on containing the WNV outbreak. Spraying in 2013 took place within range of less than 20% of infected areas.

We concluded that weather forecasts should be used to direct spraying efforts, with special attention being paid to periods of warm weather following recent rainfall. Our prediction model should be used to guide future spray campaigns, such as being linked to a frontend application for scientists and biologists to use when collecting mosquito samples. By keying in the relevant data needed as input to the model, they will be able to gauge the probability of WNV being present in the trap.

# Problem Statement

As part of the Disease And Treatment Agency, division of Societal Cures In Epidemiology and New Creative Engineering (DATA-SCIENCE), we intend to build a model that can predict where pesticides should be sprayed in the city of Chicago to counter the West Nile Virus. We will use Logistic Regression, Random Forest, K-Nearest Neighbours and the Support Vector Classifier as candidate models. The models will mainly be evaluated by their ROC AUC score and their recall score. We define a successful model as one with ROC AUC and Recall scores of at least 0.7. Lastly, we will produce a cost-benefit analysis to study the benefits of spraying pesticides versus the cost of spraying them.

# Background and Research

The WNV is the top reason for mosquito-borne disease in the continental United States area ([*source*](https://www.cdc.gov/westnile/index.html)). WNV is of particular concern in the Midwestern state of Illnois, where the case and death counts had surpassed all other states in the United States by end-2002 ([*source*](https://dph.illinois.gov/topics-services/diseases-and-conditions/west-nile-virus)). Chicago, Illinois is usually in the top 5 on Orkin's list of the Top 50 Mosquito Cities in the US ([*source*](https://www.nbcchicago.com/news/local/chicago-named-one-of-the-worst-cities-for-mosquitoes-in-us/2517461/)) \([*source*](https://www.orkin.com/press-room/orkin-releases-top-50-mosquito-cities-list)).

Approximately 1 out of every 5 people who are infected develop West Nile Fever, with the symptoms being fever, diarrhoea, vomiting, headaches, body/joint aches, rashes and swollen lymph glands ([*source*](https://www.cdc.gov/westnile/symptoms/index.html)). Frailness and exhaustion from the illness can extend to weeks or months after the onset of the fever ([*source*](https://www.cdc.gov/westnile/symptoms/index.html)). 1 out of 150 develop a severe form of disease which is neuroinvasive in nature (e.g. West Nile encephalitis, meningitis or poliomyelitis) ([*source*](https://www.who.int/news-room/fact-sheets/detail/west-nile-virus)). The symptoms include "high fever, headache, neck stiffness, stupor, disorientation, coma, tremors, convulsions, muscle weakness, vision loss, numbness and paralysis" ([*source*](https://www.who.int/news-room/fact-sheets/detail/west-nile-virus)). There may be permanent damage to the central nervous system, with approximately 1 in 10 who are seriously affected dying ([*source*](https://www.cdc.gov/westnile/symptoms/index.html)). For those who survive, it may take weeks or months to recover ([*source*](https://www.cdc.gov/westnile/symptoms/index.html)). 

Although people of all ages can get severe illness, the risk of severe illness for people above 60 increases from 1 in 150, to 1 in 50 ([*source*](https://www.cdc.gov/westnile/symptoms/index.html)). Infants and immunocompromised people are also more neurologically susceptible and at risk of death ([*source*](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4939899/)). Other examples of people in the at-risk population are those who have a history of organ transplants, or have prexisting conditions such as cancer, diabetes, hypertension and kidney disease ([*source*](https://www.cdc.gov/westnile/symptoms/index.html)).  There is currently no treatment or vaccine for WNV, only medications for symptomatic relief ([*source*](https://www.cdc.gov/westnile/healthcareproviders/healthCareProviders-TreatmentPrevention.html)). Thus, it is imperative that the problem of WNV is attended to. With respect to this, WNV is mainly tackled at the transmission stage. This entails efforts to reduce the population of mosquitoes, or limit personal exposure to mosquites (e.g. by using mosquito repellents) ([*source*](https://www.cdc.gov/westnile/healthcareproviders/healthCareProviders-TreatmentPrevention.html)). 

Transmission of WNV is most commonly spread through the bite of an infected mosquito, where the mosquitoes themselves are infected from feeding on infected birds ([*source*](https://www.cdc.gov/westnile/transmission/index.html)). Birds act as reservoirs of the virus, with the virus multiplying in their blood for several days ([*source*](https://www.who.int/news-room/fact-sheets/detail/west-nile-virus)). The virus infects over 250 bird species ([*source*](https://cwhl.vet.cornell.edu/disease/west-nile-virus)). Humans and horses are only infected, but do not act as spreaders of the virus ([*source*](https://www.who.int/news-room/fact-sheets/detail/west-nile-virus)). The exception is transmission through breastfeeding, although that is rare ([*source*](https://www.webmd.com/a-to-z-guides/west-nile-virus-faq)). Culex mosquitoes are the main vectors of the virus, especially Culex pipiens ([*source*](https://www.who.int/news-room/fact-sheets/detail/west-nile-virus)). The mosquito population is the highest in summer, and the WNV season generally reaches its height in  August and September ([*source*](https://www.webmd.com/a-to-z-guides/west-nile-virus-faq)). The mosquito season in Illinois is from early April to mid-October ([*source*](https://cristtermite.com/2021/10/when-does-mosquito-season-end-in-illinois/)).

Increased temperatures can contribute to the spread of the virus by promoting viral replication rates in mosquitoes, viral transmisison to birds, and mosquito/bird population growth ([*source*](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4342965/)). The mosquito population reduces when the temperature drops below 50°F for a prolonged length of time ([*source*](https://cristtermite.com/2021/10/when-does-mosquito-season-end-in-illinois/)). Increased precipitation and wind can promote the reproduction and migration of mosquitoes/birds, but decreased precipitation can also promote this in some cases ([*source*](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4342965/)). In a study done for Chicago, Illinois for 2004-2008, an increase in temperature was found to be the greatest temporal predictor for an increased number of infected Culex pipiens and Culex restuans mosquitoes ([*source*](https://www.vetmed.wisc.edu/goldberglab/pdf/P069.pdf)). Lower precipitation was the strongest spatial predictor ([*source*](https://www.vetmed.wisc.edu/goldberglab/pdf/P069.pdf)). For some years, a drier spring followed by a wetter summer was observed to promote WNV ([*source*](https://www.vetmed.wisc.edu/goldberglab/pdf/P069.pdf)). In another study on Chicago, it was observed that preceeding warm winters increased the probability for WNV human cases ([*source*](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0227160)). High humidity favours mosquito activity, and low humidity leads to the opposite ([*source*](https://www.orkin.com/pests/mosquitoes/when-are-mosquitoes-most-active)).

Other than solely health concerns, WNV also has major economic consequences, with the 2012 outbreak in Texas causing an estimated $47 million in losses (largely due to lost workdays) ([*source*](https://www.climatecentral.org/news/west-nile-virus-season-to-last-longer-as-climate-changes-16450)).

# Data Dictionary

## Train and Test Dataset

|Feature|Type|Description|
|---|---|---|
|**Id**|*integer*|ID of the record|
|**Date**|*string*|Date that the WNV test is performed|
|**Address**|*string*|Approximate address of the location of trap. This is sent to the GeoCoder|
|**Species**|*string*|Species of mosquitoes|
|**Block**|*float*|Block number of address|
|**Street**|*float*|Street Name|
|**Trap**|*string*|Id of the trap|
|**AddressNumberAndStreet**|*string*|Approximate address returned from GeoCoder|
|**Latitude, Longitude**|*list*|Latitude and Longitude returned from GeoCoder|
|**AddressAccuracy**|*float*|Accuracy returned from GeoCoder|
|**NumMosquitos**|*integer*|Number of mosquitoes caught in the trap|
|**WnvPresent**|*integer*|Presence of West Nile Virus in these mosquitoes. 1 means WNV is present, and 0 means not present.|

## Spray Dataset

|Feature|Type|Description|
|---|---|---|
|**Date, Time**|*string*|the date and time of the spray|
|**Latitude, Longitude**|*string*|Latitude and Longitude of the spray|

## Weather Dataset 

Weather data from 2007 to 2014. Column descriptions in noaa_weather_qclcd_documentation.pdf in the repo files folder.

## Additional Calculated Feature after Feature Engineering

|Feature|Type|Description|
|---|---|---|
|**rh**|*float*|Relative Humidity calculated from `Tavg` and `wet_bulb` feature in `Weather` Dataset.|

# Exploratory Data Analysis (EDA)

EDA was done based on the following aspects: 

* Mosquito Species
* Seasonality/ Time Periods
* Spray & trap effectiveness and locations 
* Weather impact on mosquitoes
* Temperature, Humidity, Precipitation, Wind.
  
The general insights can be found below.

## Mosquito Species

There were 7 different species of mosquitoes that were caught in the traps that were laid throughout Chicago. **3 out 7 species were WNV positive**.

## Seasonality/ Time Periods

WNV peaks in August and occurs around July to September. 

Our findings were similar to reported trends of WNV, with the peak of WNV **coinciding with summer** in Chicago and stretching into autumn (September). Warmer months in summer and early-autumn encourage mosquito propagation.

## Spray & Trap Effectiveness and Locations

It appears that spraying occurred in two main blocks. The first time was on two dates in August and September of 2011. 
The second time was a more prolonged spraying campaign, taking place over 8 dates in July, August, and September of 2013. The second spray campaign was also more intensive in terms of the number of locations sprayed. 

This was likely due to a large spike in infected mosquitos during that period, as there was a large spike in cases in August and September 2013. In 2013, 17.5% percent of traps contained WNV positive mosquitos.

However, a closer look at the year 2013 reveals that **spraying did not necessarily reduce the number of mosquitos carrying WNV**. This could have been due to the **lack of strategic planning** of trap & spray locations.

## Weather impact on mosquitoes

Temperature, Humidity, Precipitation and Wind are key environmental factors that affect the rate of mosquito growth ([*source*](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4342965/)). 

According to research, the optimal temperature for mosquito breeding is between 50 degree (minimum to be active) and 80 degree (for maximum activeness) ([*source*](https://www.mosquitosquad.com/central-illinois/about-us/blog/2018/july/how-does-weather-affect-mosquito-activity-/#:~:text=Heat%20and%20humidity&text=Temperature%20and%20mosquito%20activity%20goes,hard%20to%20function%20at%20all.)). WNV thrives in Chicago in temperatures between **55 to 80 degrees**.

The ideal humidity level of mosquitos is around **50 to 90% relative humidity**. Mosquitoes also have a 40% shorter lifespan if humidity levels were to fall below 40% and they are held without food or water.

There is an **inverse relationship between the average precipitation levels and the number of mosquitos found**. This could be due to rain disturbing stagnant waters. It could also be due to heavy rainfall which flushes eggs and larvae away, hence reducing the number of mosquitos ([source](https://www.researchgate.net/figure/Relationship-between-rainfall-and-mosquito-abundance_fig1_269767908#:~:text=Mosquitoes%20were%20more%20abundant%20during,with%20temperature%20and%20relative%20humidity.)).

For wind speed, speeds above 8.5 miles per hour reduce the number of mosquitoes ([source](https://kestrelmeters.com/blogs/news/the-science-of-mosquito-abatement#:~:text=Wind%20works%20as%20a%20natural,MPH%20wind%20gust%20is%20substantial.)). 

# Model Results

The models with their details and metrics are as follows:

|Model|Cross-validated Training ROC AUC Score|Testing ROC AUC score|Testing recall score|Testing accuracy score|
|---|---|---|---|---|
|**K-Nearest Neighbors**|0.78|0.75|0.54|0.82|
|**Random Forest**|0.79|0.77|0.25|0.90|
|**Support Vector Classifier**|0.81|0.80|0.55|0.83|
|**Logistic Regression**|0.80|0.80|0.75|0.73|

The Logistic Regression model scored better than the baseline KNN model, the Random Forest model and the SVC model in predicting whether the West Nile Virus was present in trap samples out of all trap samples with West Nile Virus. This was according to our metrics of ROC AUC and recall. It was the only model that met both our requirements (ROC AUC and recall both at least 0.7). Thus, Logistic Regression was the chosen model to classify our trap data. The cross-validation also showed that it should generalise well to unseen data. 

The accuracy scores were not the metric we were looking at, as compared to recall. The accuracy score includes predicting WNV is not there when there is no WNV, as well as predicting WNV where it is there. The imbalanced test data would make the accuracy score high. This is because it is easy to predict that there is no WNV when there is none, due to the very high number of samples with no West Nile Virus. 

Therefore, we used the recall score, which is how many positive samples were correctly identified out of all postitive samples. This would leave the negative samples out of the metric. The lower the recall, the more false negatives predicted by the model. In this case, false negatives would mean not detecting WNV where it is present, which is more serious than the opposite, false positives. With false positives, WNV is said to be present when it is not.

# Cost-Benefit Analysis

As part of the Chicago Department of Public Health (CDPH) to tackle the West Nile Virus (WNV), one of the efforts include spraying pesticides to reduce the population of mosquitioes to reduce the population of mosquitoes carrying WNV. As per our EDA, we find that the efforts for spraying pesticides were not necessarily targeted to high risk areas, possibly leading to cost-savings if our model is able to provide a prediction of high risk areas.

The costs analysed here include the cost of the spraying of pesticides, while the benefits include the cost avoidance of medical and productivity costs from preventing cases of WNV through the spraying of pesticides in Chicago. The numbers calculated were as follows:

The total cost for spraying the entire area of Chicago 14 times was $2172842 in 2021. 

The weighted medical cost for each patient was $15574 in 2021.

Spray efforts would have to reduce number of human cases by 100 in order to justify the cost of spraying the whole of Chicago every week for 3 months, but the average number of cases per year have generally been below 100. Even in 2013, which had the biggest outbreak in our dataset, there were only 66 recorded human cases ([source](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7241786/#sec009title)).

As such, spraying the whole of Chicago on a weekly basis is evidently a costly and inefficient endeavour. A more effective approach would be to target spraying at areas that have a high predicted probability of WNV outbreak.


# Conclusions

1. Presence of WNV is affected by time of year, with mosquito season peaking in July to September.
2. The three biggest weather indicators that affected the mosquito outbreak were temperature, humidity, and precipitation:
  - The ideal temperature range for mosquito breeding is 50 - 80° F
  - The ideal humidity range is a relative humidity of 64 - 83
  - Rain generally leads to less mosquitos in the short term, likely due to disturbance of stagnant water bodies. However, there is likely to be a spike in mosquitos after the rain due to creation of new stagnant water bodies.
3. Previous spray efforts have been poorly targeted. Spraying in 2013 took place within range of less than 20% of infected areas. Our EDA suggests that past spray campaigns have had limited impact on containing the WNV outbreak.

# Recommendations

1. **Monitoring should begin towards the beginning of July and last until the end of September.** This should involve tracking weather changes as well as laying traps to monitor presence of WNV in the mosquito population.
2. **Weather forecasts should be used to direct spraying efforts,** with special attention being paid to periods of warm weather following recent rainfall.
3. **Our prediction model should be used to guide future spray campaigns.** With a recall of around 75%, it presents a 55% improvement on current spray efforts, which only correctly targeted 20% of outbreak areas.


These recommendations can be integrated by exporting our Logistic Regression model to a frontend application for scientists and biologists to use when collecting mosquito samples. By keying in the relevant data needed as input to the model, we will be able to gauge the probability of WNV being present in the trap.

If WNV is present in the sample, this indicates that the particular street surrounding the trap may be a hotspot. Pesticides should thus be deployed to exterminate carriers that may be potential zoonotic vectors for the disease to spread. This achieves our objective of increasing efficiency in West Nile Virus detection and thus reducing resource wastage.

# Future Steps

- **More accurate data on weather should be gathered to input for model training and prediction.** Currently, weather data is mapped to traps depending on whether traps are nearer to station 1 or station 2. If more localized weather data can be obtained, this would greatly improve model fit and prediction.

- **Measure the efficacy of other methods of mosquito control that have been used elsewhere,** such as using larvicide, or releasing genetically-modified mosquitos. A holistic approach to mosquito control covers four key aspects ([source](https://www.epa.gov/mosquitocontrol/success-mosquito-control-integrated-approach)): 
  1. ***Removing breeding habitats*** - This involves treatment or elimination of stagnant water sources.
  2. ***Constructing structural barriers*** - Construction of screens in homes may help reduce bites.
  3. ***Controlling mosquitos at the larval stage*** - This approach maximizes the effectiveness of pesticide application and minimizes its use. One method involves use of larvicide while another method of control involves releasing genetically-modified male mosquitos that pass on genes that kill female offspring, as only female mosquitos bite and spread diseases.
  4. ***Controlling adult mosquitos*** - Using an EPA-registered pesticide is one of the fastest and best options to combat an outbreak of mosquito-borne disease being transmitted by adult mosquitoes. These pesticides are known as adulticides. Zenivex E4, which is currently used, is an adulticide.