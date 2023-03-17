# Description
During the time working as a retailer which mainly sell their product on Amazon, I was the PIC of 2 reports which is Orders and Order Detail report. 

# Context
The retailer I worked in sells products for over 7 countries mainly on Amazon. My responsibility is to create and maintain a data pipeline which is updated everydays on time and also make sure the data is always accurate for the business.

![image](https://user-images.githubusercontent.com/72678942/225907439-c7820d23-ea37-4fcd-93c9-ba86d87e1ccc.png)

# Data Pipeline Diagrams
For the last step since I mainly want to see how different of data over a period of time, I use Google Sheet for making dashboard.

![image](https://user-images.githubusercontent.com/72678942/225909789-9dd6dcd5-00ab-4430-9cde-86365e3c8dc1.png)

# Collect data from Amazon using API.
Basically after I get enough needed data such as account and password for API, I use library python-amazon-sp-api for collecting data because it is a lot quicker than our usual way. We used to process a lot to get the final canonical url.

The next token parenthese are also very importance since Amazon only gives out maximum 100 orders per request. This token will automatically go to the "next page" to collect next 100 orders in my while loop.

![image](https://user-images.githubusercontent.com/72678942/225911144-b1be3107-2098-418a-a8a3-001b19577bcd.png)


# Cleaning data and get only needed columns
The file we got from Amazon is a json file. After goes to my code, I convert it to dictionary and use the pd.DataFrame.from_dict(pd.json_normalize(all_response), orient='columns') to quickly flatten the dictionary.

![image](https://user-images.githubusercontent.com/72678942/225912628-b6e7579a-fa7c-4ab8-afd8-6eac0408139b.png)

# Insert to DB
Since we want to make sure when we are importing data to the DB, the DA or BI team won't be able to query anything from there, we decided to insert data to two different database which is Oracle and PostgreSQL.
The order id in the Order report have to be unique, so I delete all of record that have the same order id before inserting.
The final code will be set running daily using Task Scheduler.

# Maintaining pipeline
As I have been a Data Analyst and Business Intelligence experience for over 1 year, I always build a dashboart to track my work and also get my number sense of the business. 

![image](https://user-images.githubusercontent.com/72678942/225914708-868dbc5f-ba95-486c-af42-fa14de4e7c82.png)
