### BigQuery basics demo

#### Using the web UI

1. Enable billing and create a project
	1. Go to [the developers console](http://console.developers.google.com/) and sign in to your account.
	2. Create a new project with a unique ID - this is the identifier in the cloud which you'll use to match data.
	3. Enable billing: go to your project, head down to billing & settings, then enable billing.
2. Create a new bucket in cloud storage.
	1. Make sure the bucket name is unique.
	2. Upload your data: go to the cloud storage / storage browser, then click to upload files.
3. Create a new dataset in BigQuery.
	1. In the left hand side menu, in your project, create a new dataset and give it a name.
	2. Set the dataset ID and table name.
	3. Specify the data type and data source.
		- For cloud storage: `gs://<bucketname>/<tablename>`
	4. Specify the schema
		- `<name>:<datatype>,<name2>:<datatype2>,...`
	5. Check all advanced options and upload.
4. Inspect the uploaded table attributes and start writing queries.

#### Using the command-line tool

[More information here](https://cloud.google.com/bigquery/bq-command-line-tool-quickstart)

#### Install the SDK
1. Navigate to http://developers.google.com/cloud/sdk
2. Follow the step by step guide.

#### Useful commands
- To update your command line tool: `gcloud components update`
- Authenticate: the oauth dance: `gcloud auth login`
- Specify the project
	- `gcloud config set project <project>`
	- `gcloud auth list` show logins.
	- `gcloud auth revoke` revoke access.
- List all your projects `bq ls`
- load data: `bq load <dataset>.<table> <datasource>` (where datasource is the path to your file - could be local file system or google cloud storage).
- Loading data asynchronously: `bq --nosync load <dataset>.<table> <datasource>` - This gives you a job ID - copy and paste that, then enter `bq wait <jobid>` to see the status.

[<--Back](README.md)