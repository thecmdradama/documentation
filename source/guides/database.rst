Using a Database
================

**TODO**

PostgreSQL:

Step 1. Log into your PostgreSQL server  

Step 2. Enter the below command to create the pufferpanel database
CREATE DATABASE pufferpanel;

Step 3. Enter the below command to create the pufferpanel user
CREATE USER pufferpanel WITH PASSWORD '<YourChosenPassword>';

Step 4. Grant privileges to the pufferpanel database to the pufferpanel user
GRANT ALL PRIVILEGES ON DATABASE pufferpanel TO pufferpanel;

Important: If you have the PostgreSQL server on a separate host to the panel, you will need to do the following to allow remote access to the database.

Navigate to /etc/postgresql/12/main and edit pg_hba.conf

Add the following line below "# IPv4 LAN connections:"  

host    pufferpanel     pufferpanel     192.168.0.0/16           md5

Step 5. Navigate to /etc/pufferpanel and edit the config.json. 
Change
    "database": {
      "dialect": "sqlite3",
      "url": "file:/var/lib/pufferpanel/database.db?cache=shared"
    },
To
    "database": {
      "dialect": "postgres",
      "url": "host=localhost port=5432 user=pufferpanel dbname=pufferpanel password=<YourChosenPassword>"
    },
If you are running PostgreSQL on another host, update the host to the relevant IP address
    "database": {
      "dialect": "postgres",
      "url": "host=192.168.0.1 port=5432 user=pufferpanel dbname=pufferpanel password=<YourChosenPassword>"
    },
    
Step 6. Restart the panel. PufferPanel will create the necessary tables in the Database for you.




