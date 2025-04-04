###### Vendor: Mailgun
###### Process: SQL + Python

Runs SQL Automation Job Generic Emails from 9 am - 5pm 
The job insert new letters to the LetterRequest Table 
Letter: Emails to be sent
2 Automated Jobs in Olitools 
- create-email-csv: Creates the files in /Email/output and flag those letters as processed 
- sendmail: Send the emails from those files and send them after to archive folder

TODO: Migrate to pythonic environment, tho this is fully automated so it's not priority 

How to get The emails sent according to the templates (I think)
``` SQL
SELECT lr.LetterTemplateID
	  ,lt.Description
	  ,COUNT(DISTINCT LetterRequestID) AS NumberofAccounts
FROM DB806.dbo.LetterRequest as lr
	INNER JOIN DB806.dbo.LetterTemplate AS lt 
		ON lr.LetterTemplateID = lt.LetterTemplateID
	WHERE Merged = 1
	AND RequestDate > '2025-04-02'
	GROUP BY lr.LetterTemplateID, lt.Description
	ORDER BY lr.LetterTemplateID
```