# Managing Data demo

- Access control
- BQ setup
- BQ management

## Access control

#### Share dataset

To view a shared dataset (it will not display in your drop-downs by default) - dropdown, swith to project, display project.

#### BQ setup

- `gcloud auth list` shows all authenticated accounts.
- `gcloud config set project` set the project
- `gcloud config set account=me@gmail.com` switches to a given account
- `gcloud config set project myproject` sets the current project
- `gcloud ls myproject` lists all the datasets in your current project
- `bq init` - sets the default project in your BQ rc file

#### BQ management

- `bq cp publicdata:samples.shakespeare shakespeare` copies the public shakespeare table into the currently active project.
- `bq show shakespeare` shows the table data
- `bq --format=prettyjson show shakespeare` 
- `bq --format=prettyjson show shakespeare >> shakespeare_schema.json` outputs the database schema for the shakespeare table from the CLI.
	- Once this is done - you can add a new record into the schema and play with it as required.
- `bq update --expiration=900 shakespeare` - sets an expiration time on the table (15 mins in this case)
- `bq head -n 10 shakespeare` looks at the top 10 rows of the given table
- `bq help` provides a list of all the top level commands.