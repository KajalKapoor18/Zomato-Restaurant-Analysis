# Zomato Restaurant Analysis (Power BI)

An interactive Power BI dashboard analysing Zomato restaurant data across 15 countries, covering rating quality, popularity, service availability and local pricing.

## Objective
To understand how restaurants perform on Zomato: how ratings are distributed, how many restaurants are unrated, which cities and restaurants stand out within a country, and how price relates to rating.

## Data model
A star schema with one center table and two dimensions:

Table with Role:
 **Restaurants**- One row per restaurant: name, rating, votes, cost, price range, delivery and booking flags 
 **Dim_Location**-City Key, City, Country Code, Country (country names merged from the Excel file) 
 **Dim_Rating**-Rating text with a sort order (Not rated → Excellent) 

Both relationships are one-to-many, single direction, from the dimension to Restaurants.

## Data cleaning and preparation (Power Query)
- Fixed file encoding and set correct data types
- Merged country names from `Country-Code.xlsx` into the location dimension
- Created a unique City Key (Country Code + City), because city names repeat across countries
- Treated a rating of 0 as **"Not rated"**, not as a bad rating, and excluded these from all average ratings
- Kept cost in **local currency** and analysed it only within one country, so currencies are never mixed
- Used a minimum of 20 rated restaurants for the country-level average rating (`Avg Rating (Min 20)`) to avoid small-sample distortion


## Dashboard

### Page 1: Global Overview
Shows the size of the dataset (restaurants, countries, votes), the average rating, the share of unrated restaurants, the rating mix, restaurants by country and a map of average rating by country. Slicers filter by country, city and online delivery.

### Page 2: Restaurant Performance
A country-level drill-down. It shows the top cities by average cost, the relationship between cost, rating and restaurant count by city, and a restaurant-level table with city, online delivery status and rating.

## Key findings

**Global Overview** *
1. **The average rating is 3.47 out of 5**, calculated on rated restaurants only. The rating mix is mostly mid-range: "Average" is the largest category at about 38%.
2. **Only about 15% of restaurants reach "Very Good" or "Excellent"** (about 11% Very Good and 4% Excellent), while "Poor" is a very small share. Ratings cluster in the middle instead of at the extremes.
3. **About 29% of restaurants are unrated.** If these zeros had been averaged in, the mean rating would have been pulled down sharply, which is why they are excluded from rating averages.
4. **The dataset covers 15 countries but is heavily concentrated in India**, so country comparisons need a minimum sample size to be meaningful.
5. **The 7,095 restaurants in this view have 981K votes in total**, which shows that engagement is widespread across the dataset and not limited to a few listings.

## Limitations
- The data is a past snapshot with no dates, so no trends over time.
- Costs are in local currency, so cost is never compared across countries. 
- Ratings come from the Zomato scraped data and depend on the number of votes; small cities may have few ratings.
- Findings for a single country, such as Australia, rest on a small number of restaurants.

## Tools
Power BI Desktop · Power Query · DAX · Star-schema data modelling

## How to open
Download `Zomato_Analysis.pbix` from this repository and open it in Power BI Desktop. Get the dataset from the Kaggle link above if you want to refresh the data.
