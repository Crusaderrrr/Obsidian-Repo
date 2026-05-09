**Step 0** `fillDbWithZips()`:
- based on the `.csv` file with patterns
- makes api requests to the US site 
- Fetches real zip codes with some metadata (geolocation, etc.)
- Populates the db with those codes

**Step 1**:
- creates 4 parallel `ZipSplitterRunner`
- creates a queue, populated with zips from the database (step 0)
- executes all runners, which:
- each independently `synchronized` takes a zip from queue 
- makes api request to the same service using longitude and latitude of the zip and a 25 mile radius
- for every adviser that is not in the db it creates a `Customer` instance (entity) and puts it into db
	crd is used to check if investor is in db, which is a unique identifier assigned by FINRA

*IMP*: if the parser stops - delete the `_connector` tables and then start (otherwise startup will take eternity because db will re-check the connectors)

**Step 2**:
- takes a customer (investor) from the queue
- makes an api call using crd
- extracts and saves the company 
- extracts and saves office address 
- links address to the investor 
- updates status of the investor