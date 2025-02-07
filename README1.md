
Initial Load (Full Load)
	•	If the Iceberg table does not exist, it creates it by:
	•	Reading the CSV file from S3.
	•	Assigning start_date, end_date, is_active fields.
	•	Writing the data to Iceberg.

Incremental Load (CDC + SCD Type 2)
	•	If the Iceberg table already exists, it:
	•	Reads the new source CSV file from S3.
	•	Reads the existing Iceberg table.
	•	Detects changes:
	•	New records → Insert with start_date and is_active=True.
	•	Changed records → Mark old records as inactive (end_date set).
	•	Insert new versions of changed records (start_date reset).
	•	Writes the updated dataset back to Iceberg.
