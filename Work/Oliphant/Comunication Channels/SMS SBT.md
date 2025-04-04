Generate SMS per templates in a SQL Automation Job and submit those via Syncovery to the SBT FTP
Automation - SBT - Special Campaigns - OPTIN - Payment Reminders Job Steps
- Step 1 - Payment Reminders/ BP
- Step 2 - Opt-in Messages
- Step 3 - Special Campaigns 
- Rule Out New York Zip codes
- Restrict ppl in 2 way conversations 
- Avoid States that we cannot work (Massachusetts - not allowed / HW & AL - Time zone Difference therefore another script is ran)
- Get Phone actives and not Opt-out
- Get Different Templates (Legal, Special, Tax, etc)
Note To test how many sms are going to be sent without saving to SBT_campaingFile:
	run from New York check to where #Inventory is being created, Commands to check:
	SELECT * FROM #insert WHERE newtemplateid is not null  order by letterdate
	Don't forget to drop the Temporary Tables 
	DROP TABLE #INSERT,#Inventory,#OFFER,#Address,#Prelegal,#NY,#Restriction,#Active,#Special
	Is good to Run this once a day before The job Starts Running to predict SMS Generation 
To get the amount of SMS sent per Template run:
```
SELECT TemplateID
	,COUNT(DISTINCT UniqueID) AS NumberofAccounts
FROM AIM.dbo.SBT_CampaignFile
WHERE EntryDate = CAST(GETDATE() AS DATE)
GROUP BY TemplateID  
ORDER BY TemplateID
```