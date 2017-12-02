# Final Project: Food Deserts

## Question:
“Food Desert” is a long-lasting issue in metropolitans and has attracted much attention because the poor local food environment might deteriorate health status of local people. Both the growth of large supermarkets in outskirts and the economic segregation led to limited access to healthy food in inner cities. And a diet with less nutrition provided by not large supermarkets but fast food restaurants could make health outcomes poor.

Our goal is to get the correlation or causality between health outcomes and food access from the data in Chicago. The U.S. Department of Agriculture defines a food desert as an area with a poverty rate of at least 20 percent and where at least a third of the population lives more than a mile from a supermarket or large grocery store. There has been some amount of research on food deserts (Renee E. Walker et al, 2010 etc.), but we don’t know the exact number of people living in food deserts in Chicago. The new law (HB3157) approved in September requires Illinois to track food deserts, and the City of Chicago is pursuing solutions such as the collaboration with Whole Foods to solve the problem. Thus, it is a good timing to reconsider the importance of the policy.


## Datasets:
We mainly used two datasets, which have the data on locations of grocery stores and the data on the public health data including hospitalizations of chronic diseases. Both the data can be extracted from Chicago Data Portal at the format of CSV or JSON.
     
A. Grocery Stores 2011 (491 samples)
https://data.cityofchicago.org/Community-Economic-Development/Grocery-Stores-2011/4u6w-irs9

B. Public Health Statistics- Diabetes hospitalizations in Chicago, 2000 - 2011 (49 samples)
https://data.cityofchicago.org/Health-Human-Services/Public-Health-Statistics-Diabetes-hospitalizations/vekt-28b5

C. Public Health Statistics- Selected public health indicators by Chicago community area (77 samples)
https://data.cityofchicago.org/Health-Human-Services/Public-Health-Statistics-Selected-public-health-in/iqnk-2tcu

D. American Community Survey 5-Year Data (2009-2015) housing units (DP04-0001E)
https://api.census.gov/data/2015/acs/acs5/profile/variables.html

E. Boundaries - Zip Codes (2016)
https://data.cityofchicago.org/Facilities-Geographic-Boundaries/Boundaries-ZIP-Codes/gdcf-axmw

F. Boundaries - Boundaries - Community Areas (current)
https://data.cityofchicago.org/Facilities-Geographic-Boundaries/Boundaries-Community-Areas-current-/cauq-8yn6

G. Census Data A (Zip Codes, Households, Mean Income, Race, Ethnicity)
https://api.census.gov/data/2015/acs/acs5/profile?get=DP03_0051E,DP03_0063E,DP05_0028E,DP05_0033E,DP05_0066E&for=zip%20code%20tabulation%20area:*

H. Census Data B (Zip Codes, Education)
https://api.census.gov/data/2015/acs/acs5?get=B16010_001E,B16010_041E&for=zip%20code%20tabulation%20area:*

Files for these data sets can also be found in our [repository](https://github.com/a-artola/final-project-FD).

The majority of the analysis used Dataset A, B and C. Dataset A contains ZIP codes which allowed us to merge the file with Dataset B. ZIP codes were the only geographic data in Dataset B. Dataset C contains data at the Census Community Area level (defined as homogeneous neighborhood-like districts - 77 in Chicago) which is likely to produce more accurate results; however, it provides only diabetes related mortality from 2007. So, our analysis only included data from Dataset B.

Dataset D provided data on housing units per zip code and zip code land area. This allowed us to determine the square footage of grocery stores per square mile in each zip code. Datasets E and F provided GIS data for mapping our results. Datasets G and H provided control variables for our regressions.


## Results:

All code for this analysis can be found in the following jupyter notebook: [food_desert_coding.ipynb](https://github.com/a-artola/final-project-FD/blob/master/food_desert_coding.ipynb)

Our analysis focused on two variables: Grocery Store Density and Diabetes Hospitalization Rate. Grocery Store Density was calculated in two ways. We calculated the density percentage taking the aggregated square footage of grocery stores per ZIP code over the land area of the ZIP code. We also aggregated the number of grocery stores in each ZIP code. Diabetes Hospitalization Rate is the  number of hospital discharges attributed to residents of each ZIP code divided by the total population for the zip code. For this analysis, we used the adjusted rate which controls for the effects of differences in population age distributions.

#### Grocery Store Density (%) and Hospitalization Rate (%):
![hosprate_grocdens](https://user-images.githubusercontent.com/32336614/33510911-f7ad43fc-d6d7-11e7-8dce-c243e481c365.png)

#### Grocery Store Density (N) and Hospitalization Rate (%):
![hosprate_grocdens_n](https://user-images.githubusercontent.com/32336614/33510914-f99ed612-d6d7-11e7-9df8-268287dec181.png)

#### Fast Food Restaurant (N) and Hospitalization Rate ($):
![hosprate_fastf_n](https://user-images.githubusercontent.com/32336614/33510916-fb6c74e0-d6d7-11e7-927c-79394b2ca57c.png)

As we expected, the larger area is occupied by grocery stores, the less people suffer from diabetes. However, the health outcome does not seem to depend on how many grocery stores are in a district. More fast food restaurants do not appear to increase the hospitalization rate. This might be because the inner city in Chicago has many fast food restaurants and wealthy people who are likely to be healthy. See figures above.

#### Covariate Regressions:
<img width="455" alt="screen shot 2017-12-01 at 10 00 12 pm" src="https://user-images.githubusercontent.com/32336614/33511602-2f62abba-d6e3-11e7-885d-9f3a5c725569.png">

For our regressions, we included mean income, race, ethnicity and higher education attainment.

The coefficients of grocery store density, fast food shop density and mean incomes are not significant because their t-values are not so large. On the other hand, the race composition explains the healthcare outcome of diabetes better. 

#### Distribution of Grocery Stores:
<img src="https://user-images.githubusercontent.com/32336614/33511279-86eda50c-d6dd-11e7-8fcc-b6672259ae07.png" height="450" alt="Blue Dots">

To further analyze the presence of food deserts in Chicago, we plotted grocery store locations according to their relative size. We included size in the plot to give more weight to larger supermarkets compared to convenient stores and other smaller stores that might not actually sell a variety of healthy foods. From these map we can see geographic trends in the distribution of grocery stores.

### Food Deserts:
Now, remember the definition of "food desert".

The U.S. Department of Agriculture describes that a food desert is an area with a poverty rate of at least 20 percent and where at least a third of the population lives more than a mile from a supermarket or large grocery store.However, if we follow the definition, there are almost no places which satisfy the conditions in Chicago. Therefore, suppose that we lower the threshold of distance from a grocery to 1km instead of 1mile(=1.6km) while we keep the threshold of poverty rates in the area. We can obtain the data of "poverty rates" from Census.

<img src="https://user-images.githubusercontent.com/32336614/33512042-4723d0f8-d6ed-11e7-90b5-0c526817f398.png" height="450" alt="food_des1">

To visualize the accessibility to closest groceries, we can also depict a map with gradation.

<img src="https://user-images.githubusercontent.com/32336614/33512043-48cf79de-d6ed-11e7-8365-eb9fa7ac92f2.png" height="450" alt="food_des2">

#### Grocery Store Density (%) and Hospitalization Rate (%) by ZIP code:
<img src="https://user-images.githubusercontent.com/32336614/33511445-92668806-d6e0-11e7-8131-27935fadfacc.png" height="290" alt="groc_cens"><img src="https://user-images.githubusercontent.com/32336614/33510925-4a695c3e-d6d8-11e7-82cc-a03acd115d52.png" height="290" alt="diabetes_cens"><img src="https://user-images.githubusercontent.com/32336614/33510927-4aa981c4-d6d8-11e7-994f-36307e780054.png" height="290" alt="blue_red">

After plotting grocery store density and hospitalization rates by ZIP code, we can see where any overlap exists (or doesn't). "Grocery Store Square Feet per Square and Diabetes Hospitalization Rate" shows patches of dark purple which represents areas in which there is both a low grocery store density and a high rate of diabetes. This occurs on the south side and it is particularly concentrated on the west side. The North West corner of the city has very low grocery store density but also very low rates of diabetes. In the North East corner, we see the opposite: higher rates of diabetes and very high grocery store density.


## Limitations:

Our analysis would have benefited from diabetes statistics at either a Census Community Area level or a Census Tract Level. This would have allowed us analyze health levels closer to the locations of the food deserts. Also, our analysis was not as robust as possible. Other factors that relate to socioeconomic status and the geography of the city would have benefited the analysis. Moreover, our analysis suffered from a small sample size. 


## Conclusion:

Although our analysis cannot corroborate the bad effects of food deserts, we cannot make any assertions as to whether a relationship does or does not exist between health outcomes and food deserts. Therefore, we expect further research on food desert's influence on health in the area with more samples and a more robust set of covariates.


