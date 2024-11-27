OFAC Database Load: 
- Read data from SDN.xml list
- Check Date 
- Convert to Json for easy read 
- Load Reference Value Sets
- Load Locations 
- Load ID Reg Locations
- Load Distinct Parties
- Load Sanctions Entries
- Load Profile Relationships
OFAC Schema DB [[SDN.excalidraw]]

KYC OFAC Checks:
- Email and Phone:
	- Email search in ofac_feature where feature_type_id = 21
	- Phone search in ofac_feature where feature_type_id = 524
- CustomerAddress
	- Google Maps Api to validate the address
	- Search Street field in LocationPartValue that the location_part.type == Address; Consider in the future adding A2 A3 ...
	- Search City field in LocationPartValue that the location_part.type == City;
	- Search State.name field in LocationPartValue that the location_part.type == State
- First Name, Last Name
	- First Name search in ofac_documented_name_part where documented_name.alias.alias_type = 1403 and name_part_group.name_part_type = 1520
	- Last Name the same but name_part_type = 1521
	- If middle name is present apply name_part_type = 1522
- SSN, (ID Document)
	- Check SSN field in OFACIDRegDocument.id_reg_doc_type == SSN and matches IDRegistrationNo to user ssn input, Same with the other types of documents (Passport, ID, etc)

Transaction Monitoring OFAC Checks:
- AuthApi check Location 
	- Merchant Data merchant_country 
	- 
	
OFAC Report:
-  Create Word Document with the information about the OFAC coincidences found 

Transaction Monitoring
- Check in auth api
	- Merchant Country and block not allowed ones
	- Search for coincidences for merchant description in OFACDocumentedNamePart that their name_part_group name_part_type_id == 1525 (Entity Names)

Merchants Risk Feature
- Each Merchant ID will be registered in the Merchant Risk Model with a score 

Monitoring Internal Transfers
- Internal Transfers does not require OFAC check, all the recipients are registered in kredio and OFAC checks were processed in them
	- Review only the memo, if it contains the keywords for the OFAC entities then cancel the transfer 
- Zelle and Cashapp still pending
- OFAC for Recipients, FN, LN, Phone, Email

1 - Fuzzy logic algorithms for transaction clustering to prevent structuring
	- Logic Implemented in Card Load, Cash Deposits and Check Deposit
	- Card Load is started by Galileo Auth Api and Cash/Check Deposit by Kredio
	- The system will run a check for every incoming transaction of those types, will check for the previous 20 days deposits if the sum of those transactions is greater than $10000 it will raise a Flag: Stacking Transactions Alert for account ACC_ID, Total: Amount and cancel the incoming transaction
2 - Detecting continuous deposits and withdrawals in short period
	 - Logic implemented in ATM Withdrawals, Card Load, Cash Deposits and Check Deposits
	 - Card Load and ATM Withdrawals is started by Galileo Auth Api and Cash/Check Deposit by Kredio
	 - There are account Limits for certain those actions in a certain period of time that can be different between users for example a user can only perform 10 ATM withdrawals every month, once that limit is Reached it will raise a flag Flag: 10 Card Load Deposits detected in 5 days for account ACC_ID. Same logic for the other cases
3 - Activity involving offshore jurisdictions
	   - OFAC checks to check the entity 
	   - Also if the Country is not in the allowed Countries raise a flag Flag: Alert in transaction: Country Tajikistan Not Allowed