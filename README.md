# OVERVIEW
This repository contains Big Query code using Google Analytics raw data that will provide a summary of the Google Analytics data. The data studio dashboard (https://datastudio.google.com/reporting/78e5657c-ac77-4fd9-a2ba-e620bb083c0b) brings many of the insights to life around performance through the lens of user behavior timing. 

This solution utilizes `device.time_zone_offset_seconds` to analyze performance in the **user's actual local time**.

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
4. The By-Day-By-Hour Big Query code provided, create and save the view in Big Query
5. Make a copy of the data studio dashboard and connect it to the saved view

# THE WATCH-OUTS
The key Watch-Outs: 

1. The most critical step is having Google Analytics connected to Big Query, the By-Day-By-Hour is using the default schema in Big Query + E-commerce events which will require setting up in Google Tag Manager to provide the insights 
2. It's important to have the right architecture setup. The above shared GitHub GTM link helps with the architecture if a deeper aduit of events etc is needed
3. Conversion Rate will need to be added as a calculated metric - SUM(purchases)/SUM(sessions)
4. Add To Cart Rate will need to be added as a calculated metric - SUM(adds_to_cart) / SUM(sessions)
5. Cart Completion Rate will need to be added as a calculated metric - SUM(purchases) / SUM(adds_to_cart)
6. Revenue Per Session will need to be added as a calculated metric - SUM(total_revenue) / SUM(sessions)

