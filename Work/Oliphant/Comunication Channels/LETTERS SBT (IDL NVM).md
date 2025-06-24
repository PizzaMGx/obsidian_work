Old Process: 
	Add the Letters in LetterRequest Table 
	Add the Campaings in SBTCampaignFile Table

JOB - Automation - SBT Insert IDL Occurs every day every 30 minute(s) between 10:15:00 AM and 4:30:59 PM
JOB - Automation - SBT Process IDL Occurs every day every 10 minute(s) between 9:40:00 AM and 5:31:00 PM

Olitools Generate Letters
	- Ecol_lettergen lettergen function 
		- param - letterrequest_id
	- First Query 
```sql
SELECT * FROM [DB806].[dbo].[LetterRequest] WHERE LetterTemplateID = {} AND Merged = 0
```
	- Second Query using the result of the first one (We can just merge this in one query)
```sql
	SELECT * FROM [Maintenance].[dbo].[LetterTemplate] WHERE LetterTemplateID = {}
```
	- Third Query to call a sproc to create the Letter Requests
```sql
USE [DB806]
DECLARE	@return_value int
EXEC	@return_value = [dbo].[usp_LetterMergeFields_Standard_USA]
		@AccountID = {},
		@PersonID = {},
		@PostDatedTransID = NULL,
		@TransactionID = NULL,
		@PromiseID = NULL,
		@LetterRequestID = {}
SELECT	'Return Value' = @return_value
```


BA get_letter_request shared Celery Task:
	- Gets the csv files in /automation/SBT/Letters
	- Runs this query to get the Letter Requests images 
```SQL
SELECT * FROM AIM.dbo.SBT_CampaignFile cf
INNER JOIN DB806.dbo.LetterRequest lr ON cf.LetterRequestID = lr.LetterRequestID
WHERE lr.SentToVendor = 0
AND lr.MergeError IS NULL
AND lr.MergedLetter IS NOT NULL
AND cf.CampaignFileID in (CampaignFileID in csvfiles)
```
	- Convert the MergedLetter field of the request letters into Images 
	- Images are sent to /automation/SBT/Files/
	- CSV Files are sent to /automation/SBT/Campaign/
	- Images were being picked by SBT 

Then I guess a syncovery Job will handle the rest
