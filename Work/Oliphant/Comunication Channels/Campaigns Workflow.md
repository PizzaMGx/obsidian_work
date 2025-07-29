Tables 
- Activity
- SMS_Messages
- SMS_MessageType
- SMS_CampaignSchedule
- SMS_CampaignType

How do we queue Campaigns 
usp_OliTools_SMSCampaignQueue sproc

How I think it is:
We queue Activities with the NextActivityID = 2270 which does not correspond to any Message Template but rather to queue an activity for that account
SMS_campaignType is The type of Campaign (Outreach, Tax Time, etc)
Schedule Campaign with SMS_CampaignSchedule and define the amount of days it going to run

In the sproc usp_OliTools_SMSCampaignQueue We get all the activities queued and iterate over them, then create 




