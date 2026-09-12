# CSV Ingestion process

# With Docker and your system

- Download the csv dataset from kaggle - (url - https://www.kaggle.com/datasets/datasetengineer/logistics-and-supply-chain-dataset)

- put the csv into your project codebase

- we have to make a docker container which will run MSSQL server
  Configurations for docker
  First create the volume
  docker volume create mssql_data

# Then run this script

```
docker run -e "ACCEPT_EULA=Y" \
 -e "MSSQL_SA_PASSWORD=YourStrong@Password123" \
 -p 1433:1433 \
 --name mssql2022 \
 --restart unless-stopped \
 -v mssql_data:/var/opt/mssql \
 -d mcr.microsoft.com/mssql/server:2022-latest
```

# This will make a MSSQL db server

# Now we have to ingest the csv data into db

- make a script for ingestion and run (python scripts/ingest_csv_data_into_db.py)

- now the db connection is done and all the csv data is pushed into db

- connect with db through vs code extension - mssql

# Configurations

Profile Name: legacy-mssql
Server name*: localhost
Port: 1433
Trust server certificate: 🟩 Check this box / turn it ON (Crucial for Docker)
Authentication type*: SQL Login
User name*: sa
Password*: Your Password
Save Password: 🟩 Check this box
Database name: Type master (or leave it on "Select a database")
Encrypt: ⚠️ Change this from Mandatory to Optional (or False)

- After connecting to db you can check the connection by running query inside VS code
- Do CTRL + N and then change the Plain Text to SQL
- and then you can write the query
  SELECT \* FROM dbo.TBL_SC_FLEET_HIST_RAW;

# With AWS and Docker inside it

Instance type : c7i-flex.large
storage : 30 gb
ubuntu (linux)
Security group > attach the security while creating ec2 instance
Launch instance
SSH using .pem file from your system
install the docker

# Then run this script

```
docker run -e "ACCEPT_EULA=Y" \
 -e "MSSQL_SA_PASSWORD=YourStrong@Password123" \
 -p 1433:1433 \
 --name mssql2022 \
 --restart unless-stopped \
 -v mssql_data:/var/opt/mssql \
 -d mcr.microsoft.com/mssql/server:2022-latest
```

copy the ip address of the ec2 (public) and paste the ip address inside you env (SQL_SERVER_HOST)
On this public IP my sql server will be running
