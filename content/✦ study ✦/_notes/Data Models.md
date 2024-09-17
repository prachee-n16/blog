1. Data at Rest Model
	- Example: Data stored in databases, data warehouses or other storage mediums
	- Views data in **resting** state; bounded sets of data accessed on ad-hoc or scheduled basis
		- Batch processing: Process data continuously requiring several trips to storage layer; high latency and slow decision making
	- Stores current snapshot of system; loses intermediate state changes
2. Data in Motion Model
	- Example: Social media feeds, financial transactions
		- Gives rise to [[Streaming data platform|streaming data platforms]] 
	- Views data as infinite and fast-moving data streams
 
