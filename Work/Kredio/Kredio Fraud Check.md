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
- CustomerAddress
	- Google Maps Api to validate the address
	- Search Street field in LocationPartValue that the location_part.type == Address; Consider in the future adding A2 A3 ...
	- Search City field in LocationPartValue that the location_part.type == City;
	- Search State.name field in LocationPartValue that the location_part.type == State
- First Name, Last Name
	- Search FirstName, LastName in Identity where AliasType == Name, DocumentedName With different NamePartValue.NamePartGroup.NamePartType == FirstName and Last Name, NamePartValue.Value = First Name, Last Name
- SSN, (ID Document)
	- Check SSN field in OFACIDRegDocument.id_reg_doc_type == SSN and matches IDRegistrationNo to user ssn input, Same with the other types of documents (Passport, ID, etc)

Transaction Monitoring OFAC Checks:
- AuthApi check Location 
	- Merchant Data merchant_country 
	
OFAC Report:

