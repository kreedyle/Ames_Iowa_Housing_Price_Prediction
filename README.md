## Project 2: Ames Housing Dataset Analysis: Regression

### Problem statement: 

A renovation company has hired you as a data analyst to determine what feature(s) of a home add the most value to them. The information from the presentation will be used to develop talking points for sales reps and also pamphlets/leaflets to pass out around town. This project focuses mainly on the features with quality attributes - more specifically kitchens and fireplaces. 

### Data Chosen: 
----
- [`train.csv`](../data/train.csv): Ames Housing Data Train Set
- [`test.csv`](../data/test.csv): Ames Housing Data Test Set
------
### Outside research/inspirations: 

Resources used:
https://medium.com/diogo-menezes-borges/project-2-predicting-house-prices-on-kaggle-989f1b0c4ef6

https://medium.com/towards-data-science/everything-you-need-to-know-about-multicollinearity-2f21f082d6dc

https://towardsdatascience.com/transforming-skewed-data-73da4c2d0d16

https://medium.com/towards-data-science/predicting-home-prices-in-ames-iowa-3a247e6c9639
-----
### Data Dictionary


* saleprice - the property's sale price in dollars. This is the target variable that you're trying to predict for this challenge. (int64)

* overall_quality: Overall material and finish quality (int64)
    - 10 Very Excellent
    - 9 Excellent
    - 8 Very Good
    - 7 Good
    - 6 Above Average
    - 5 Average
    - 4 Below Average
    - 3 Fair
    - 2 Poor
    - 1 Very Poor
* year_built: Original construction date (int64)

* year_remodeled: Remodel date (same as construction date if no remodeling or additions) (int64)

* square_footage: * first_floor_sf: First Floor square feet + second_floor_sf: Second floor square feet + * total_bsmt_sf: Total square feet of basement area (float64)

* fireplaces: Number of fireplaces (int64)

* fireplace_quality: Fireplace quality (uint8)
    - Ex Excellent - Exceptional Masonry Fireplace
    - Gd Good - Masonry Fireplace in main level
    - TA Average - Prefabricated Fireplace in main living area or Masonry Fireplace in basement
    - Fa Fair - Prefabricated Fireplace in basement
    - Po Poor - Ben Franklin Stove
    - NA No Fireplace
# Encoded before modeling
*    fireplace_quality_Ex      uint8
*   fireplace_quality_Fa      uint8
*    fireplace_quality_Gd      uint8
*   fireplace_quality_Po      uint8
*    fireplace_quality_TA      uint8
# Encoded before modeling
* kitchen: Number of kitchens(int64)
* kitchen_quality: Kitchen quality (uint8)
    - Ex Excellent
    - Gd Good
    - TA Typical/Average
    - Fa Fair
    - Po Poor
* kitchen_quality_Ex        uint8
* kitchen_quality_Fa        uint8
* kitchen_quality_Gd        uint8
* kitchen_quality_TA        uint8

-----
### Overview of Data Dictionary: 
As my problem statement was concerned with inference and seeing which features would add the most value to a home, I only ended up using 17 columns - 14 of which were numeric while the other three were categorical features. Therefore, I wrote a function to encode them before modeling. 


-----
### Conclusions, keytakeaways, recommendations

Upon more EDA and based off their correlation to sale price, I have decided the two features I will examine in my model will be kitchens and fireplaces. The necessity of a kitchen in a home guarantees an ever available market of clients needing small improvements like fixtures or a complete overall of cabinetry. Furthermore, the asthetic and charm a fireplace adds to a home is unique and eye catching. Another factor to consider about the opportunities for fireplace renovations is close to half of the homes in our data set have at least one fireplace - further analysis of the data could produce a target market based off neighborhood or house age.  

In my initial search, I was certain fireplaces would have a higher coefficient which equates to a higher added value to the sale price of the home. As the quality measure of these features improves, the average sale price increases for fireplaces the average increase is ~$45,000 and for kitchens ~$72,331. Considering most homeowners pay around $2,314 for a fireplace installation and between $4,000 to $34,962 for a kitchen remodel depending on size, materials and complexity. The ratio of installation to added value seems more than worth the investment. 

However, I want to speak about the scoring and coefficients of what my linear model produced. My best performing model  was RidgeCV being able to accurately predict prices within $27,218 for the training set and ~$31,000 for the validation set. Furthermore, the model is able to predict close to 20% of the variance in sale price. The coefficients show us how much the expected sale price would increase by improving the quality features of either the kitchen or fireplace. A kitchen renovated from average quality to excellent would increase the sale price by as much as ~$55,000 and a fireplace from poor to excellent quality would increase the sale price by as much as $19,000. 

Overall, my model performed well given the low amount of features I chose to use; however, the features I chose were based off thorough EDA as to which features could potentially add value to a home. After the analysis of renovation type features, I would like to dig into the patterns which may emerge when looking at the neighborhood column. From a quick iteration of dummying the neighborhood variable and joining with sale price, square footage, and overall quality, the coefficients with the greatest effect on price were: Edwards & Old Town with a negative correlation of 6,261 & 7,845 respectively and the neighborhood of North Ridge Heights & Stone Brick having coefficients of 13,416 & 8,105 respectively.

As we determined earlier, I believe the best strategy as of right now would be to examine which neighborhoods had a  majority of their houses built between the late '90s and early 2000's such as College Circle, Timber, and Gilbert to name a few.

On things I could improve, I would like to figure out why when charting average sale price to feature quality the numbers were drastically different. Furthermore, perfecting pipeline and onehotencoder to make the iterations of my model easier is where I need to learn to grow in. 