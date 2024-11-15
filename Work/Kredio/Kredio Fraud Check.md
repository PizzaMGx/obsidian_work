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