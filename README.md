# final-project-Food Desert

# Question:
“Food Desert” is a long-lasting issue in metropolitans and has attracted much attention because the poor local food environment might deteriorate health status of local people. Both the growth of large supermarkets in outskirts and the economic segregation led to limited access to healthy food in inner cities. And a diet with less nutrition provided by not large supermarkets but fast food restaurants could make health outcomes poor.

Our goal is to get the correlation or causality between health outcomes and food access from the data in Chicago. The U.S. Department of Agriculture defines a food desert as an area with a poverty rate of at least 20 percent and where at least a third of the population lives more than a mile from a supermarket or large grocery store. There has been some amount of research on food deserts (Renee E. Walker et al, 2010 etc.), but we don’t know the exact number of people living in food deserts in Chicago. The new law (HB3157) approved last month requires Illinois to track food deserts, and the City of Chicago is pursuing solutions such as the collaboration with Whole Foods to solve the problem. Thus, it is a good timing to reconsider the importance of the policy.


# Datasets:
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

Files for these data sets can also be found in our [repository](https://github.com/phobosgt3/final-project-FD).

The majority of the analysis used Dataset A, B and C. Dataset A contains ZIP codes which allowed us to merge the file with Dataset B. ZIP codes were the only geographic data in Dataset B. Dataset C contains data at the Census Community Area level (defined as homogeneous neighborhood-like districts - 77 in Chicago) which is likely to produce more accurate results; however, it provides only diabetes related mortality from 2007. So, our analysis only included data from Dataset B.

Dataset D provided data on housing units per zip code and zip code land area. This allowed us to determine the square footage of grocery stores per square mile in each zip code. Datasets E and F provided GIS data for mapping our results. Datasets G and H provided control variables for our regressions.


# Investigation:

All code for this analysis can be found in the following jupyter notebook:

[food_desert_coding.ipynb](https://github.com/phobosgt3/final-project-FD/blob/master/food_desert_coding.ipynb)

## Results: 

Our analysis focused on two variables: Grocery Store Density and Diabetes Hospitalization Rate. Grocery Store Density was calculated in two ways. We caclulated the percentage taking the aggregated square footage of grocery store per ZIP code over the land area of the ZIP code. We also calculated the number of grocery stores in each ZIP code. Diabeted Hospitalization Rate is the  number of hospital discharges attributed to residents of each ZIP code divided by the total population for the zip code. For this analysis, we used the adjusted rate which controls for the effects of differences in population age distributions.

### Grocery Store Density (%) and Hospitalization Rate (%):
![hosprate_grocdens](https://user-images.githubusercontent.com/32336614/33510911-f7ad43fc-d6d7-11e7-8dce-c243e481c365.png)

### Grocery Store Density (N) and Hospitalization Rate (%):
![hosprate_grocdens_n](https://user-images.githubusercontent.com/32336614/33510914-f99ed612-d6d7-11e7-9df8-268287dec181.png)

### Fast Food Restaurant (N) and Hospitalization Rate ($):
![hosprate_fastf_n](https://user-images.githubusercontent.com/32336614/33510916-fb6c74e0-d6d7-11e7-927c-79394b2ca57c.png)

### Distribution of Grocery Stores:
![blue_dots](https://user-images.githubusercontent.com/32336614/33511279-86eda50c-d6dd-11e7-8fcc-b6672259ae07.png)

### Grocery Store Density by ZIP code:
![groc_cens](https://user-images.githubusercontent.com/32336614/33510928-4ac70532-d6d8-11e7-9bbf-131efd5cbd78.png)

### Hospitalization Rate ($) by ZIP code:
![diabetes_cens](https://user-images.githubusercontent.com/32336614/33510925-4a695c3e-d6d8-11e7-82cc-a03acd115d52.png)

### Grocery Store Density and Hospitalization Rate ($) Quartile Comparison:
![groc_hosp_quar](https://user-images.githubusercontent.com/32336614/33510929-4ae30746-d6d8-11e7-877d-fbc54e50b21c.png)

### Grocery Store Density and Hospitalization Rate ($) Overlap:
![blue_red](https://user-images.githubusercontent.com/32336614/33510927-4aa981c4-d6d8-11e7-994f-36307e780054.png)

# Limitations:

# Conclusion:


