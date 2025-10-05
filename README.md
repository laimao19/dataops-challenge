# N1 Health - Data Ops Challenge
## Description
N1 Health’s client, a national Medicare Advantage plan, is seeking to understand how best to use its resources to address food access challenges in its membership. N1 Health has been tasked with presenting a short analysis (~5-10 minutes) of publicly available data to the Chief Medical Officer to answer this question.

## Research/Guiding Questions
1.	Where should we deploy a food access program?
2.	How many people will be included? How many might be successfully engaged?
3.	Which subgroup of the population might benefit the most from the program?
4.	What is the projected impact of this program?

## Research about the Topic
- What is a medicare advantage plan?
    - According to the uhc website, "Medicare Advantage (Part C) plans offer all the benefits of Original Medicare (Part A and Part B), with extras like dental, vision, and hearing benefits. Some offer health and wellness benefits, like a gym membership. Most include part D prescription drug coverage."
    - Major providers that offer these plans include UnitedHealthcare, Humana, Aetna, Cigna, etc.
    - "Medicare is federal health insurance for anyone **age 65 and older**, and some people under 65 with certain disabilities or conditions."
- What could be defined as a "food access challenge"?
    - The following information is taken from the straydoginstitute website on food access disparities
    - **Food access**: "the stable availability of nourishing, affordable, and suitable foods. physical and economic accessibility are important elements, along with production systems that prioritize the wellbeing of food producers and consumers"
    - **Common food access challenges**: corporate control of food and agriculture, poverty and unemployment, institutionalized racism, inequitable healthcare access, and weather and climate instability
    - **Why is food access important?**: "although humans can survive on nutritionally poor foods, nutritionally inadequate diets are linked to numerous chronic health conditions that can worse quality of life, impair mobility, increase acute illnesses such as cancer, and shorten lifespan"
- What would we want to target in relation to "best using its resources" for this national medicare advantage plan?
    - target **geographic areas** with the biggest need (counties/cities where a lot of people have trouble getting healthy food AND where diet-related health problems are high)
    - target **members most at risk**  which would be lower-income adults with chronic conditions where a bad diet would make things worse, possibly SNAP households and seniors in rural areas who cant travel

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
        - It seems like if data was missing, it is just missing as a NULL from the dataset.
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
- CORGIS County Demographics CSV File (https://corgis-edu.github.io/corgis/csv/county_demographics/)
    - Gives information "about counties in the United States from 2010 through 2019 through the United States Census Bureau"
    - Includes a variable that is an "estimated percentage of population whose ages are equal or greater than 65 years old" for various County, State places in the United States
    - Values are denoted as -1 in this dataset if they are not available.
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
- **Additional Important Information**: Regarding the actual challenge.db file that was given
    - I used the DB Browser (SQLite) to browse through the actual .db file and observe what was given
    - For the 500 cities dataset -> I believe all columns that are listed on the website are provided in this data
    - For the FDA Food Atlas dataset -> only the "Access" sub-dataset is given as well as the variable list that provides meanings for each of the keys
    - Table names:
        - five_hundred_cities = 500 cities
        - access = access subtable in FDA food atlas
        - variable_list = variable list subtable in FDA food atlas
    - Another thing I noticed was that in the actual given FDA food atlas access table, the FIPS code is sometimes 4 digits and is sometimes 5 digits. It's 4 digits when the first digit would have been 0, and 5 digits when the first digit is not 0. 

## Evaluation Criteria
- Can you produce a compelling analytical story from novel, messy datasets?
- Can you communicate these results to a non-technical audience?
- 2-3 key data visualizations to answer the questions detailed in the description
- Create a short presentation with about 5 slides to show your results
