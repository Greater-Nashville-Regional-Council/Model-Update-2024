# Model Update 2024

*Employment Baseline Methodology*

Woods and Poole “2023” forecasts are created with projected employment numbers beginning in 2021 as this is when they significantly deviate from the Bureau of Economic Analysis’ county level employment data (table CAEMP25N: Total full-time and part-time employment by NAICS industry). The need for an adjusted baseline comes from the fact that in many cases, the 2022 BEA data (at this time the latest CAEMP25N release) was significantly higher than the 2023 Woods and Poole data. In order to adjust for this, 2022 BEA data is put in the place of the 2022 Woods and Poole data, suppressed employment numbers are imputed, the employment numbers between 2022 and 2050 are smoothed, and then the BEA employment categories are redistributed to NAICS categories. Despite the name of the BEA dataset indicating that jobs are categorized entirely by NAICS categories, there is a slight but important difference in categorization. BEA codes put all employment for government owned establishments into code 2000: “Government and government enterprises”, subs of which are 2001: “Federal Civilian”, 2002: “Military”, and “2010”: “State and Local”. NAICS codes distribute non Public-Administration employment at government owned establishments into other categories such as Educational Services and Waste Remediation, etc. The final goal of the employment baseline is the distribution of employment to Census blocks. The step-by-step methodology is outlined below.

Bring in two datasets: 2022 BEA employment data by industry by county, and 2022 Woods and Poole employment data by industry by county. 

The categories for both are as follows: 

Total employment (number of jobs): 10, Farm: 70, Forestry, fishing and related activities: 100, Mining, quarrying, and oil and gas extraction: 200,  Utilities: 300, Construction: 400, Manufacturing: 500, Wholesale trade: 600, Retail trade: 700, Transportation and warehousing: 800, Information: 900, Finance and insurance: 1000, Real estate and rental and leasing: 1100, Professional, scientific, and technical services: 1200, Management of companies and enterprises: 1300, Administrative and support and waste management and remediation services: 1400, Educational services: 1500, Health care and social assistance: 1600, Arts, entertainment, and recreation: 1700, Accommodation and food services: 1800, Other services (except government and government enterprises): 1900,  Federal Civilian Government: 2001, Military: 2002, and State and Local: 2010.

*Initial Baseline*

BEA employment data gives a good view of as many jobs as possible down to the county level. This data incorporates information from many sources. The primary input is the Bureau of Labor Statistics’ Quarterly Census of Employment and Wages – which is an industry standard for employment as it is derived from unemployment insurance filings. This dataset also encompasses sole-proprietor employment as well as railroad and religious employment. One drawback to its use is that if there are too few establishments in a county, that industry will be suppressed. This was the case for many of the 2022 disaggregated counties. The first step was to impute this data using the relationship between the BEA and Woods and Poole datasets. The suppressed industries were identified in the BEA data, and then the corresponding industries identified in the Woods and Poole data. The Woods and Poole corresponding industries were summed to represent “suppressed employment”, and then the shares that they represented of the total were multiplied by the difference between the total BEA employment and the non-suppressed BEA employment. This gives us a baseline number for each industry per county that adds up to the initial BEA 2022 data.

*Industry Aggregation*

Next the industries are grouped to more closely match the NAICS 2 digit categories. Federal civilian, Military, and State and Local employment is aggregated to represent “Government”, which is later distributed across industries. Farm and Forestry, fishing, and related activities are grouped to represent NAICS 11: Agriculture, forestry, fishing and hunting.

*Smoothing*

Once this baseline is completed, it is used to smooth the county/two digit industry employment between 2022 and 2050. The formula is below:

year_adjusted_value = year_initial_value – (baseyear_woodspoole_value –baseyear_baseline_value)/
(finalyear_int – baseyear_int)*(finalyear_int – year_int)

For example, with base year of 2022 having values both from the previously adjusted baseline and the unadjusted Woods and Poole raw data, the calculation for industry x in county y for 2045 would be:
2045 adjusted employment = 2045 non-adjusted employment – (2022 Woods and Poole employment – 2022 Baseline employment)/(2050 – 2022) * (2050 – 2045)
Government Distribution
The distribution of establishment ownership per county per industry is from JobsEQ (Chmura Economics). This dataset also uses QCEW as its main input which includes private sector covered employees, federal, state, and local government employees. This dataset also includes unincorporated self-employed workers derived from the Current Population Survey, non-covered railroad workers derived from annual Railroad Retirement Act and Railroad Unemployment Insurance Act data provided by the United States Railroad Retirement Board, as well as non-covered religious organizations derived from both the BLS Current Employment Statistics and Census County Business Patterns. The railroad and religious employees are grouped off and added to private sector employment. The final distribution is the total percent of employment in private sector establishments, government establishments, and self-employment. 
This distribution is used to see the share of employment per industry per geography per year that is based in a government establishment. The assumption is that this distribution will be relatively consistent across years. 
“Public Administration” is a NAICS category that is not present in the BEA categories. It is taken to be the difference between the BEA “Government” employment and all of the government employment (total industry employment multiplied by the “share of industry that is government employment”) that is outside of the “Government” industry. 
Employment at government owned establishments by industry is then taken as a share of the total “Government” industry employment (BEA Category). Then this is used to multiply the initial BEA “Government” industry employment out to the NAICS categories. 
Mantissa Round
As this data is distributed to the NAICS categories, it must be rounded so that each employment baseline represents a discrete number of jobs. Each year of data is mantissa rounded at the individual county level.
Distribution to Census Blocks
To distribute these employment totals to blocks, the LEHD (Longitudinal Employer-Household Dynamics) was used. This is a product of the Center for Economic Studies at the US Census Bureau. Specifically, the LODES (Origin-Destination Employment Statistics), where LODES 8.1 was prepared for release in October of 2023 representing year 2021. This is the most reliable, recent release of disaggregated place-of-work data by industry.
All two digit NAICS categories, except for Educational Services, are collected by block. Educational Services is typically tagged to a school administration office rather than the location of the educational facility, so in this case for a location-based model this was subbed in from DataAxel. All these 2-digit categories were re-summed due to this replacement, and then a distribution is created per industry per block by the county control totals per industry.
This framework is then used to distribute whatever year of data is necessary to examine by block. In this case 2023 is the base year of our model. These are mantissa rounded as well to represent discrete jobs. 

