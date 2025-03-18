Metrics Automated Campains Creation based on the users that lgged in and didnt made a payment

Script File:
[olphnt / olitools / ecol_controllers / ecol_metrics.py — Bitbucket](https://bitbucket.org/olphnt/olitools/src/master/ecol_controllers/ecol_metrics.py)

Steps: 
	1 Pull Data from Matomo Metrics Website using Matomo Api 
	2 Get Users that logged in in the past 70 minutes and did not made a payment, for that get the actions details that includes login and excludes payment_submit
	3 Submit the data to livevox to Create a Campaign so the agents can call those Customers
	3.1 Get Microsoft Oauth Token with to submit to livevox Session Api
	3.2 Get Livevox Session Token the Oauth for sso
	3.3 Create Csv File with the user Data 
	3.4 Submit the file to Create New Campaign, Wait 10 seconds to Build and Activate 
	4 Run the process in Rundeck in a hourly Schedule