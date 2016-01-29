https://www.cbtnuggets.com/it-training/google-bigquery-qualified-developer/2?autostart=1

# Google BigQuery notes

## Introduction video

### Video Outline

- Google & big data
- Bigquery overview
- Bigquery big picture

## Google and big data

Big data challenges

- Scaling up is expensive
- Scaling up is error prone
- Scaling up has limitations
- Traditional methods didn't cut it. 

Google wanted to be self reliant, so they scaled out. Bought a fleet of commodity machines so failure was the norm.

3 core technologies. Google's big data stack 1.0

1. Google File System (GFS). Core concept = fail all the time. Replicate data across the cluster so failure isn't a problem.
2. MapReduce. Slow & difficult - needs a lot of skills.
3. BigTable - sits on top of GFS. A key-value store (key being the URL, value being all the information). BigTable sits underneath a lot of Google products out there. Problems come up in multi-centre environment.

BigTable is the grandfather of NoSQL - MongoDB, etc.

Due to the problems with Google's big data stack 1.0, they built out new technologies.

1. Megastore - strong consistency on top of BigTable. If data goes through megastore to get into BigTable, it has to be hardened, committed to get in there.
2. Spanner - "the next iteration of megastore". Does everything Megastore does, but on a planet-wide scale. Google installed GPS and atomic clocks in every data centre, to fix timing issues.
3. Dremel - Came about because Google Engineers had a hard time getting answers using MapReduce. Engineers wanted a SQL-like interface to get quick answers from their data centres.
4. Colossus - not a lot know at this stage as it's a new technology. This is GFS version 2. Has all but replaced GFS.

Stack 1: all about batch processing.
Stack 2: all about real-time processing.

#### What is BigQuery?

BigQuery is the public implementation of Dremel.
Fully-managed data analysis service for large datasets.
Reliable, secure, scalable, friendly and extremely fast.
Uses a multi-level execution tree to dispatch queries and aggregate results across 1000s of machines.

#### Why use it?

- Fast, cheap interaction with big data.
- Generating big data reports requires skilled people. Anyone with SQL can use it.
- BigQuery redefines big data analytics. Importing, exporting and shaping data is simplified.

#### BigQuery Vs MapReduce
MapReduce is at the start of the pipeline, transforming the data. Batch processing.
BigQuery is for near real-time analytics.

#### End-to-end workflow
Data goes into Cloud Storage - imported from database / log files / other. Computed in Transformed into meaningful format using MapReduce / compute engine into a format BigQuery can understand.

BigQuery provides a user-friendly front end to access this data.

biquery-samples - a ton of example datasets.

## BigQuery Basics video

### Video Outline

- BigQuery Use Case
- BigQuery Pipeline to analysis
- BigQuery Fundamentals
- Accessing BigQuery

### BigQuery Use Case: Safari Books.

Safari Books online. Have billions of records of usage data. 
[More information here.](http://cbt.gg/1o0xM0e)

#### Goals / benefits 

1. Business dashboards & trend analysis.
2. Sales intelligence & automatic lead generation. e.g. matching user browsing history to transactions 
3. Fast ad-hoc answers for specific business questions.

#### Challenges

1. Existing MySQL infrastructure too slow.
2. Hadoop required too many resources to maintain.



### Pipeline to analysis

--DIAGRAM-- big data pipeline and analysis on the google cloud platform.

1. Data in CRM, RDBMS, Log files, etc.
2. Use ETL tools to transform data
3. Get data into Google Cloud storage.
	- Use object change notification - as soon as files in cloud storage update, BigQuery can automatically pull them in.
4. [Optional] Use Hadoop or MapReduce to run additional transformation steps.
5. Send data over to BigQuery. 
6. Use Google Data visualisation tools OR 
7. Use 3rd party data visualisation e.g. Tableau.

### BigQuery fundamentals

- Project: Container for users, APIs, authentication & billing
- Dataset: a container for tables. Lowest level for applying access control.
- Table: the data containers
	- Schemas: every table has one. Defined on creation. Each one has:
		- Name (field name)
		- Type (data type: string, float, integer, etc.)
		- Mode: nullable, required, repeated.
- Column ... of a table.

#### Data formats

- CSV
- JSON

### Accessing BigQuery

- BigQuery interactive web UI. Great management / development tool.
- Command line tool (BQ). Python tool. Allows us to do everything in the web UI tool and more. We can create scripts to automate the commmon management stuff.
- [REST API:](http://developers.google.com/apis-explorer) build applications & tools which hit BigQuery through the REST API. 
- 3rd party tools: visualisation tools (e.g. [BIME](http://www.bimeanalytics.com/)), loading tools, direct connect tools.






