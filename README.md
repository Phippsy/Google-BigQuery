# Google BigQuery notes

### Course Outline

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



