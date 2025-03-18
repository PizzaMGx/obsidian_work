Stream Lit , Matplotlib
Create New container but use the django models to manage the data. (Like celery)

Graph to Show Transactions over time 
- Settled Transactions 
- Per User and Period
	Transaction Amount, dt_when 
	- 1 Year Period
	- 1 Month Period
-  Map To show Time and Location to track user movements, App login, POS for better visualization
- Graph data structure to detect money mules, Points Graph to show money movement starting from User Node then it ends Billpay, POS, and other non Person 2 Person Transfer, otherwise another node will be created as children and same process of filtering transactions 
	- Keep in mind double Linked Nodes <----> 
	- Also Amount of Transactions and money can be implemented as weight values
	- Implement Reverse Search as well, from a user get all the sender "Parent" nodes

