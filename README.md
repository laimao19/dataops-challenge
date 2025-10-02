# N1 Health - Data Ops Challenge
## Description
N1 Health’s client, a national Medicare Advantage plan, is seeking to understand how best to use its resources to address food access challenges in its membership. N1 Health has been tasked with presenting a short analysis (~5-10 minutes) of publicly available data to the Chief Medical Officer to answer this question.

## Research/Guiding Question Answers
1.	Where should we deploy a food access program?
    - [answer]
2.	How many people will be included? How many might be successfully engaged?
    - [answer]
3.	Which subgroup of the population might benefit the most from the program?
    - [answer]
4.	What is the projected impact of this program?
    - [answer]

## Datasets for Analysis
- CDC - 500 Cities Project
    - Contains state, city, and population information about different areas in the USA (500 cities)
    - Coupled with each city, we get information about prevalence of different health-related points within various age ranges (usually just >= 18 years but sometimes with more specifications or >= 65 years):
        - current lack of health insurance
        - arthritis
        - binge drinking
        - high blood pressure
        - taking medicine for high blood pressure
        - cancer (excluding skin cancer)
        - current asthma
        - coronary heart disease
        - visits to doctor for routine checkup
        - cholesterol screening
        -  etc.
    - **Keywords to understand**:
        - crude prevalence: raw percentage not adjusted for differences in age, distribution, demographics, etc.
        - confidence interval: tells the range in which the true percentage is expected to fall (likely 95% of the time)
    - **How did they deal with missing data?**
- FDA - Food Atlas
    - Purpose of this dataset/atlas is to "provide a spatial overview of a community's ability to access healthy food and its success in doing so" and "to assemble statistics on food environment indicators to stimulate research on the determinants of food choices and diet quality"
    - Contains information about the state, county, and FIPS codes (federal information standard publication code)
    - Mainly contains information and specific codes about:
        - access and proximity to food stores (for different demographics, e.g. SNAP households, low income, etc.)
        - store availabilities (dollar stores, convenience stores, etc.)
        - restaurant availabilties
        - food assistance participants
        - local foods informations (farmers markets, vegetable farms, etc.)
        - etc.
    - Varying units used for the aforementioned information (% change, count, percent, # per 1,000 pop)
    - **How did they deal with missing data?**
        - "Data that were not available, not applicable, or suppresssed for specific counties are denoted with N/A or -9999. Counties that didn't exist in a particular year are referred to with -8888."
- **Additional Important Information**: FIPS
    - What is FIPS?
        - Federal Information Processing System (FIPS) Codes for States and Counties
        - Numbers that uniquely identify geographic areas
    - Specifics
        - State-level codes have two digits
        - County-level codes have five digits of which the first two are the FIPS code of the state to which the county belongs
    - Related to the datasets
        - 500 cities dataset has both the city FIPS code ("placefips") and tract FIPS code ("tractfips")
        - FDA dataset uses only the county-level FIPS code ("FIPS")
        - **NOTE**: the FDA dataset's county-level code and 500 cities dataset's city-level code DO NOT match. the first 5 digits of the tract FIPS code for the 500 cities dataset DOES match the convention of the FDA dataset codes though.
        
## Evaluation Criteria
- Can you produce a compelling analytical story from novel, messy datasets?
- Can you communicate these results to a non-technical audience?
- 2-3 key data visualizations to answer the questions detailed in the description
- Create a short presentation with about 5 slides to show your results
