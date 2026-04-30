# OVERVIEW
This repository contains Big Query code using Google Analytics raw data that will provide a summary of the Google Analytics data. The data studio dashboard (https://datastudio.google.com/reporting/78e5657c-ac77-4fd9-a2ba-e620bb083c0b) brings many of the insights to life around performance through the lens of user behavior timing. 

Standard reporting which often defaults to UTC or a single property timezone, this solution utilizes `device.time_zone_offset_seconds` to analyze performance in the **user's actual local time**.

## DAY PART DEFINITIONS
The data is segmented into the following buckets:
* **Early Risers**: 4 AM - 5 AM
* **Breakfast**: 6 AM - 9 AM
* **Morning**: 10 AM - 11 AM
* **Lunchtime**: 12 PM - 2 PM
* **Afternoon**: 3 PM - 4 PM
* **Early Evening**: 5 PM - 7 PM
* **Evening**: 8 PM - 11 PM
* **Lates**: 12 AM - 3 AM

(the segmentation can be easily tweaked that match the business model requirements) 

# THE SET-UP
The steps required:

1. To be able to generate the data to build the dashboard it requires implementing this GTM container > https://github.com/GTMRecipeContainers/Google-Analytics-4-Enhanced-E-commerce it will require configuring the triggers + GA4 event tag that works best for the website
3. Google Analytics is connected to Big Query
4. The 101-GA-Audit Big Query code provided, create and save the view in Big Query
5. Make a copy of the data studio dashboard and connect it to the saved view

# THE WATCH-OUTS
The key Watch-Outs: 

1. The most critical step is having Google Analytics connected to Big Query, the 101-GA-Audit is using the default schema in Big Query + purchase event which will require setting up in Google Tag Manager to provide the insights 
2. It's important to have the right architecture setup. The above shared GitHub GTM link helps with the architecture if a deeper aduit of events etc is needed
3. The Big Query code - 101-GA-Audit is the one that should be connected to the dashboard
4. The Big Query code - 101-GA-Audit-withnodatedimensions is the same as 101-GA-Audit but without the date breakdown if a deeper dive is required without dates  
5. The Big Query code - 101-GA-Audit-DuplicateTransactions tracks duplicate transactions that happen within the same session 
6. The Big Query code - 101-GA-Audit-KPIs provides a daily breakdown of key metrics
7. Conversion Rate is the only calculated metric thay will need to be added - SUM(converted_sessions)/SUM(total_sessions)

# DATA FILTERING
One of the outputs from the audit will be how to filter data to provide a better view of performance. The options would be to either filter in Biq Query (hard filter) or in Data Studio (soft filter). 

Exclude In Big Query: 

1. Spam & Bot Traffic: If you identify a surge of fake hits from a specific IP or Browser version
2. Hostname Errors: Traffic from test.shop.com or localhost
3. Ghost Transactions: Technical misfires with NULL IDs that have no business value
4. Internal Testing: Traffic from your dev team

Exclude in Data Studio: 

1. Regional Focus (e.g., Africa): If you want the option to see that data occasionally, but want the main dashboard to ignore it.
2. Product Categories: Switching between views for "Product A" vs "Product B."
3. Date Ranges: Allowing the user to toggle between Last 14 Days and Last 30 Days
4. Marketing Segments: Toggling between Organic and Paid traffic performance
