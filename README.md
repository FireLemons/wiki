## installation

A file named `.env` is required to set the database credentials. `dev.env` can be copied into `.env` to create one.

### production
#### MariaDB
A standalone mariadb has been created for this.  

First a TrueNAS dataset was created with default settings named mariadb.

The mariaDB app was installed through the TrueNAS app store using the following settings.

```
Application Name: mariadb
Version: default

Image Version: v11
User: wiki_schema
Password: password for wiki_schema
Database: wiki
Root Password: password for root
Auto Upgrade: off
Additional Environment Variables: empty

Port Bind Mode: Publish port on the host for external access
Port Number: default
Host IPs: empty
Networks: empty

Data Storage Type: Host Path
Host Path: Path to the dataset created earlier
Additional Storage: empty

Labels Configuration: empty

CPUs: default
Memory: 2048
```

The mariaDB user/group then needs to be given ownership of this dataset via `chown -R 999:999 /mnt/data/mariadb` from the shell.

If no `.env` file exists, `dev.env` can be copied and the following values can be editied for database access:

 - `DATABASE_HOST`: The host for the mariaDB database.
 - `MYSQL_ROOT_PASSWORD` Not required. Delete this line.
 - `WIKI_SCHEMA_PASSWORD` Change to a secure password.
 - `WIKI_APP_PASSWORD` Change to a secure password.

run `./create_users.sh` and run the output SQL into the mariaDB console.

### development
copy `dev.env` into `.env`  

docker compose --profile dev up
