OFAC Database Load: 
	Read data from SDN.xml list
	Check Date 
	Convert to Json for easy read 
	Load Reference Value Sets
	Load Locations 
	Load ID Reg Locations
	Load Distinct Parties
	Load Sanctions Entries
	Load Profile Relationships

KYC OFAC Checks:
- When User submits address (CustomerAddress model)
	- Google Maps Api to validate the address
	- Search Street field in LocationPartValue that the location_part.type == Address; Consider in the future adding A2 A3 ...
	- Search City field in LocationPartValue that the location_part.type == City;
	- Search State.name field in LocationPartValue that the location_part.type == State
- When User Submits First Name, Last Name and DOB
	- Search FirstName, LastName in Identity where AliasType == Name, NamePartValue.NamePartGroup.NamePartType == FirstName and Last Name 
- When User submits SSN, (ID Document)
	- Check SSN field in OFACIDRegDocument.id_reg_doc_type that is in "SSN" and matches id_registration_no
	
OFAC Report:

