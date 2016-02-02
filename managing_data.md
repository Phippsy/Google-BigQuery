# Managing Data

Join each and group H are useful for large data sets.

GitHub dataset live example
GitHub language popularity - pull time series by Python, r, etc

Snapshot decorator
Select repository language, count repository language as pushes
From githubarchive @-3600000000
Pulls data for 10 hours ago

Range decorator
From githubarchive @-3600000000--180000000

The minus sign makes the time relative to now

Absolute decorator
First, get the ms from th date you're looking at
Screenshot

Wildcard decorators
Select(table_query([projectname], 'table_id contains "ny"'))

Union queries
Like an rbind
You just comma separate your table names in your from clause.
Very useful to use a Wildcard query with a union query because you don't need to update code if you add new tables.

Nested and repeated data
Benefits - storage and processing benefit hugely, but queries will be a bit more complex. Also for ETL, the process will be a little more complex on nested and repeated.

Challenges
Screenshot
Add the live dataset to your project

Managing data

Access control
Tables and data
BQ CLI
Management tips

Access control
2 levels available: project and dataset.
Add users, groups or service accounts. Only possible through the web UI.
Select project in cloud console, go to permissions. Add member and choose role.

Roles
Most restrictive - least restrictive:
Can view- can start a job, --- see screenshot.

Dataset roles include special groups e.g. All authenticated users = the public.

You can add people by email, domain, all authenticated.

Generally you'll use project roles to assign to your project team. Datasets for others e.g. Public. There is no table-level ACL, only dataset level.

Tables and data
Copy: drop down in web UI. No link between source and destination tables.
CLI:

Delete: drop down in web UI.

Expire: set auto destruct. Useful for time sharding of data.

Updating tables: you can append fields or set specific properties of fields e.g. Null able, but you can change data types.

Data
There is no data modification. You can append only, and your schema must match.

Solution for frequent changes:

BQ CLI
Download sdk
Gcloud auth login
Gcloud set project
Local file is stored in $home/.config/gcloud - any problems, delete this file.

Documentation: BQ help
BQ help (command name)

--apilogswitch: view all your requests going over.

Flags
Common flags first, specific flags then follow the common flags.
Set defaults with /.bigqueryrc file.

BQ init will set up a bigqueryrc file for you. This is useful for e.g. Using a default dataset with every project.

Copy: cp source data

Management tips

Schema design: partition tables.
Cost optimisation: limit processing. Partition tables according to query patterns. Look at usage patterns to figure this out.
Expire shared tables.

Data isolation and security: if you need granular security, you. GitHub need to shard datasets ton manage access accordingly.

Performance tips: Materialise intermediate tables for frequently used sub queries, extract new columns from complex data.
Use table decorators for smaller scans. Use table wild cards for shared data, so you can create more tables that are smaller.

You can purchase more throughput if required.