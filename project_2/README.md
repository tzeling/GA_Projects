
# Project 2
## Problem Statment
Home sellers often anchor their offer price to avoid underselling, while home buyers, due to information asymmetry, often pay different prices for houses with similar features.
As a property consultancy firm, we aim to build a model to identify the features that are most important to predict sales price of houses. This would allow us to provide our clients with a tool that gives estimates of their potential selling prices, and help them identify which aspects of their properties they can improve on to enhance their selling prices.
A linear regression model will be trained with the given data, with regularisation (Ridge and Lasso regularization). The models will be evaluated based on their R-squared score and the best predictive model with the highest R-squared score will be selected. The target R-squared score was 0.8 for the chosen model.

## Background
Ames is a city in Iowa located in the Midwest region of the United States. It is home to Iowa State University with around half the population being students. Combined with the fact that there are many job opportunities, this would attract a young professionals to Ames ([*source*](https://www.cityofames.org/about-ames/about-ames)).

As more people work remotely due to the pandemic, a growing number of people are looking to move from larger cities in favour of smaller and cosier towns. As such, we expect demand for housing in Ames to grow in line with the current trends ([*source*](https://www.mymove.com/moving/covid-19/coronavirus-moving-trends/)). For homeowners in Ames looking to sell their property, it is important to understand which features of the house contributes the most to home prices in order to optimise their home value.

In the housing market, the pricing is determined by the intrinsic property attributes, as well as the local neighbourhood environment in which it resides ([*source*](https://www.investopedia.com/terms/h/hedonicpricing.asp)). This method is known as hedonic pricing method.

The hedonic pricing method is applied in real estate through the valuation of a house intrinsic features - such as size of the house, type of house and the physical condition of the house - as well as local environment attributes - such as environmental quality(e.g. air quality, noise pollution, water quality), and amenities(e.g. schools, malls, eateries) ([*source*](https://www.ecosystemvaluation.org/hedonic_pricing.htm)).

Some popular ways to get an indication of home value include ([*source*](https://www.opendoor.com/w/blog/factors-that-influence-home-value)):
* Knowing the transcation price of houses sold in the same neighbourhood recently
* Determining what facilities are in the vincinity
* Calculating the livable space of the house
* Knowing the age and condition of the house
* Having remodelled or upgraded the house recently

## Executive Summary
The housing market in Iowa has been on the rise. As more home sellers and buyers look to buy and sell homes, our property consultancy firm aims to build a model to help predict the sales price of house in Ames, Iowa. Through exploratory analysis of the data, we have found that various factors such as quality, area and age of the house are some of the predictive features of the value of the property.
Linear regression with Ridge and Lasso Regularisation were evaluated. The data was split into training and testing sets. The target was to achieve an R-squared score of at least 0.8. Out of the 3 models, linear regression with ridge regularisation performed the best with an R-squared score of 0.88.
We recommend prospective home sellers to consider the following recommendations:
Since quality in general is a feature highly regarded by homebuyers, including external quality and kitchen quality. This suggests that some buyers may be looking to buy ready to move-in homes, some ways to improve house price would be to ensure the house has good exterior coverings and a kitchen of high quality.
Bonus features like bathrooms or fireplaces would boost sale prices too.

## Datasets selected:
* [`train.csv`](./data/train.csv): Training Ames Housing Dataset
* [`test.csv`](./data/test.csv): Test Ames Housing Dataset

## Data Dictionary
|Feature|Type|Dataset|Description|
|---|---|---|---|
|lot_area|int|train-final|Lot size in square feet|
|alley|int|train-final|Type of alley access to property|
|lot_shape|float|train-final|General shape of property|
|land_contour|object|train-final|Flatness of the property|
|lot_config|object|train-final|Lot configuration|
|land_slope|float|train-final|Slope of property|
|neighborhood|object|train-final|Physical locations within Ames city limits|
|condition_1|object|train-final|Proximity to various conditions|
|condition_2|object|train-final|Proximity to various conditions (if more than one is present)|
|overall_qual|int|train-final|Rates the overall material and finish of the house|
|overall_cond|int|train-final|Rates the overall condition of the house|
|year_remod/add|int|train-final|Remodel status|
|exterior_1st|object|train-final|Exterior covering on house|
|exterior_2nd|object|train-final|Exterior covering on house (if more than one material)|
|exter_qual|float|train-final|Evaluates the quality of the material on the exterior|
|exter_cond|float|train-final|Evaluates the present condition of the material on the exterior|
|foundation|object|train-final|Type of foundation|
|bsmt_qual|float|train-final|Evaluates the height of the basement|
|bsmt_cond|float|train-final|Evaluates the general condition of the basement|
|bsmt_exposure|float|train-final|Refers to walkout or garden level walls|
|bsmtfin_type_1|float|train-final|Rating of basement finished area|
|bsmtfin_type_2|float|train-final|Rating of basement finished area (if multiple types)|
|total_bsmt_sf|float|train-final|Total square feet of basement area|
|heating|object|train-final|Type of heating|
|central_air|int|train-final|Central air conditioning|
|electrical|float|train-final|Electrical system|
|gr_liv_area|int|train-final|Above grade (ground) living area square feet|
|kitchen_qual|float|train-final|Kitchen quality|
|functional|float|train-final|Home functionality (Assume typical unless deductions are warranted)|
|fireplaces|int|train-final|Number of fireplaces|
|garage_area|float|train-final|Size of garage in square feet|
|garage_qual|float|train-final|Garage quality|
|garage_cond|float|train-final|Garage condition|
|paved_drive|float|train-final|Paved driveway|
|wood_deck_sf|int|train-final|Wood deck area in square feet|
|fence|int|train-final|Refers to presence of fence|
|saleprice|int|train-final|Sale price|
|age|int|train-final|Age of property at time of sale|
|pool|int|train-final|Refers to presence of pool|
|rm_count|int|train-final|Total room count|
|bath_count|float|train-final|Total bathroom count|
|num_floors|float|train-final|Total number of floors|
|porch_area|int|train-final|Total porch area|


## Findings:
Measure of Area:
* 'Gr_liv_area' has a high positive correlation with sale price, indicating that the size of living area is an important factor for determining sale price.
* A similar trend can be seen for 'total_bsmt_sf' and 'garage_area' signalling that potential homebuyers would want a garage and basement.
* A weaker positive correlation can be seen for 'porch_area' indicating that though some homebuyers may prefer having a porch, it may not be the top priority for them.
Quality:
* Generally all the measures of quality have a positive correlation with sale price. Having higher quality in different areas of the house will result in an increase in sale price.
Age:
* There is a negative correlation between age and sale price, which may be attributed to the deterioration of the house as time passes.
Neighbourhoods:
* Houses in these neighbourhood fetches the highest sale price: 'StoneBr', 'NridgHt'
* Houses in these neighbourhood fetches the lowest sale price: 'BrDale', 'MeadowV', 'IDOTRR'
* 'BrDale', 'MeadowV', 'NPkVill' have a narrow sale price range


## Conclusions and Recommendations
Ridge Regression performed the best with with a cross validiation score at 82.7% and the test $R^2$ score of 87.3%.

**Most valuable features:**
* Neighbourhood
* Land contour (hillside)
* Proximity to positive off-site feature--park, greenbelt, etc.
* External quality (including exterior covering on the house, with brick common being the most preferred)
* Kitchen quality

**Consideration for home owners:**

Location seems to be the most important feature that prospective homebuyers look at. Neighbourhoods that fetch a higher price include Stone Brook, Northridge Heights and Northridge. These neighbourhoods tend to be located quite centrally within Ames, possibly providing convience to different amenities, hence leading to high sale prices.
Additionally, houses on a hillside seems to provide a boost in sale price. A possible reason is that it provides more privacy, and would be suitable for buyers who prefer a more quiet surrounding.
Houses within close proximity to positive off-site features such as parks or greenbelts commanded a higher price. There are several reasons for this, having a park or greenbelt improves the view from the house, and provides a convenient alternative from having to go to a rural area to get the same experience. It also serves as a social space where families, friends and communities can gather.
Quality in general is another feature highly regarded by homebuyers, including external quality and kitchen quality. This suggests that some buyers may be looking to buy ready to move-in homes, some ways to improve house price would be to ensure the house has good exterior coverings and a kitchen of high quality.
Finally, bonus features like bathrooms or fireplaces would boost sale prices too.

**Moving forward:**
There are 2 main ways to improve the model moving forward:
1. Evaluate proximity to amenities
* Since location is a top feature, data collection of proximity to amenities(such as supermarkets, schools or restaurants) could be done to further narrow down the neighbourhood features that have a high correlation with sale prices of properties. 
2. Intangible features
* Features that increases the quality of one’s life, which may rival the location of the property as the most important feature for the purchase of a property. For example, the safety index & crime rate of the neighborhood, transport accessibility, and noise & air quality.