###### Vendor: DropCowboys
###### Process: SQL + Python + Livevox

##### **SQL Sproc: Maintenance usp_AUT_DropCowboyQueueCampaigns** 
- Grabs the elegible accounts to send a Voicemail
- Creates Files in the automation/DropCowboy folder
- Creates File in the automation/DropCowboy/LivevoxDNC to create Do not call Lists
Procedure tips: Comment out the union with settlement accounts if less accounts are required (around line 300)
Schedule: Running manually, usually at 10 am EST time

SQL Explanation:
- First as an optional Step we populate a SIF table for bigger Volume
- 

##### **Python Scripts: Olitools/ecol_dropcowboys process_campaigns_dp  - Olitools/ecol_metrics create_dnc_livevox** 
- First Script grabs the files in the automation/DropCowboy folder and sends the voicemails to the respective phone numbers
- Sends the files to the automation/DropCowboy/Archive folder
- Second Script grabs the files in the automation/DropCowboy/LivevoxDNC folder and creates the DNC lists in livevox using Livevox Api 
Schedule: Runs every hour 

##### **Monitoring Tool Python: Business Assist/flask_celery/monitoring_tasks monitor_voicemails**
- Runs At 5, 7, 11 pm UTC Time (EST - 4) 
- Checks goal to reach 5000, 20000 and 50000 respectively 
- Sends Email to Team when the goal is not reached

##### **TODO:**
- Add create dnc in Rundeck with the process campaign process 
- Move SQL to Python as much as possible for full automation and Better Data Parsing
- Monitor Tools not only sends email 

###### Vendor: Voapps
###### Process: SQL + Python

Not Too Important For now, Document later