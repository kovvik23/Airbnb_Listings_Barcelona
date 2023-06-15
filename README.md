# Barcelona Airbnb Listings Analysis

## Overview

This project provides an analysis of the Barcelona Airbnb listings for a period of 12 months between March 2023 and February 2024. The data was sourced from [http://insideairbnb.com/get-the-data/](http://insideairbnb.com/get-the-data/) on 11 June 2023. The project utilized the "listings" and "calendar" CSV files from the website, which were compiled into a single Microsoft Excel file, then visualized in a dashboard using Tableau.

## Data Processing

1. **Data Cleaning:**
During the inspection of the data, the following observations were made:
   - The location information only included GPS coordinates, not the address or the postcode.
   -> To address this, the CSV files were first converted to XLSX format and the Geocoding API was used to obtain the postcode from the GPS coordinates.
   - Once the data had been converted to XLSX, there was some inconsistent formatting of the latitude and longitude data - some data was formatted as text with a comma used as the decimal separator, while some were formatted as numbers including a decimal point. The GPS data was cleaned and made consistent.

2. **Obtaining Postcode using Geocoding API:**
   - The `WEBSERVICE` function was utilized in Microsoft Excel to make an API call to retrieve the relevant data.
   - Example formula: `=WEBSERVICE("https://maps.googleapis.com/maps/api/geocode/xml?latlng=latitude,longitude&key=API_key")`
   - Extraction of the postcode from the API output was done using a formula that parsed the XML data.
   - Example formula: `=INDEX(FILTERXML(cell_with_API_output, "//result[type='street_address']/address_component[type='postal_code']/long_name"), 1)`

Some of the filtering resulted in `#VALUE!` errors as not all location data had a `street_address` result. In these cases, data was further parsed to a different result, and the postcode was extracted from there.

3. **Postcode Formatting:**
   - Due to formatting limitations and the fact that Barcelona postcodes begin with the character "0," further data manipulation was required following the postcode extraction step. This was achieved by concatenation.

## Data Visualization

The cleaned and processed data was visualized using Tableau. A dashboard was created to illustrate various aspects for individuals interested in investing in a Barcelona property with the intention of listing and renting it on Airbnb.

The dashboard can be accessed at [this link](https://public.tableau.com/views/BarcelonaAirbnbprojectdashboard/Dashboard1?:language=en-GB&publish=yes&:display_count=n&:origin=viz_share_link). A PDF version of the dashboard is also available in this repository.

## Data Observations

Based on the visualizations and summaries derived from the data, the following observations were made:

- The average price by postcode bar chart and map visualizations reveal that the top five postcodes associated with the highest revenue from listings during the observed time period are 08003, 08013, 08025, 08011, and 08037. This information, along with geographical and touristic considerations, can aid an investment decisions and provide a good primary overview of the price analysis by neighborhood.

- Similarly, the average total price visualized by neighborhood group (distrito) in a bar chart indicates potential areas where investments are likely to yield good returns. This serves as an initial step before conducting further targeted analysis.

- The line chart depicts the revenue trends over a 12-month period, spanning from 14 March 2023, to February 2024, providing valuable insights. It is worth noting that the chart has been filtered to exclude a couple of weeks of data in March 2024, as it significantly skewed the line chart. However, it is important to acknowledge another skew in the visualization of the data which was not excluded from the chart. March 2023 exhibits a significantly lower total price for listings compared to other months, which may be attributed to the limited data available for that particular month (2.5 weeks only). Apart from this value for March 2023, the fluctuation between months demonstrates a maximum difference of 1,000,000 euros between the highest and lowest data points. Conducting further quantitative analysis with a larger dataset spanning longer than what has been included in this analysis would be beneficial to gain deeper insights and perform a more comprehensive seasonal demand analysis.

- Revenue by room type, visualized in a bar chart, clearly suggests that entire home/apartment listings are the best sellers, while hotel rooms have the lowest interest on Airbnb. Renting out an entire apartment is recommended as a successful strategy, although considering the total revenue generated from multiple private rooms (which amounts to 54,423,325 euros in total vs 121,494,557 euros for entire homes) would be useful to analyze further before a final conclusion is to be drawn.

- The "Best selling listings by minimum stay" table highlights the top five results based on the minimum number of nights' stay vs total price. The table indicates that shorter stays ranging from 1 to 4 nights are the most popular, with 32-day minimum stays (mid-term stays) occupying the fifth position.

Further things to note: Some of the data included in the analysis extends into the future, and it is essential to consider this when drawing conclusions. While many customers tend to book in advance for popular tourist destinations like Barcelona, it is important to acknowledge that there are cases of last-minute bookings and cancellations. These last-minute changes, which are not included in this analysis, can potentially impact the findings. Therefore, it is crucial to exercise caution and recognize that the analysis may not capture the full spectrum of booking behaviors. By understanding the limitations and considering both advanced bookings and last-minute reservations, a more comprehensive understanding of the data can be achieved. 

## Conclusion
In conclusion, the analysis of the Barcelona Airbnb listings provides valuable insights into various aspects of the data. Key observations include the top postcodes associated with high revenue, the revenue trends over an approximately 12-month period, and the popularity of different room types.

Overall, this brief analysis serves as a preliminary exploration based on the available data, providing a starting point for potential in-depth analysis in the following areas:

- Price analysis by neighborhood, considering real estate prices and tourist locations.
- Occupancy rate and revenue analysis.
- Investment return analysis.
- Seasonal demand analysis with a larger dataset.
- Competitor analysis.

These additional analyses can provide more comprehensive insights and support informed decision-making.
