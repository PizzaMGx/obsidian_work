1 - Modify SMS Outbound Sproc to Match both use cases 
	- Total Collector requires Optin check 
		- Argument optin_required in the sproc
		- If optin_required then get the activities with the optin NextActivityID 
		- Also check if the person has received an optin yet
	 - We skip this for SBT 

2 - Modify Python Scheduled jobs
	- For Total Collectr pass the argument
	- Make sure all the templates work
	- Change the Campaign ID to tc_template_id
2 - Check the webhook 
	- The result matches that of SBT