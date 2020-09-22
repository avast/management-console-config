# management-console-config

## Run
Sample configuration for Avast Business management console.
1. Adjust .env file
2. run `docker-compose up`

## Upgrade from 5.X or 6.X versions to 7.X
OBC from version 7.X uses PostgreSQL version 10.4 which is not directly compatible with data from older OBC versions.
In order to use your old data, you must manually convert them by running the new DB image with following command:

```docker run -it -v afb_data:/var/lib/postgresql/data -v afb_backup:/var/lib/postgresql/backup avastsoftware/management-console-db:10.4.2 /usr/bin/upgrade-pg-9-to-10.sh```

**Notes:**
* Make sure you have enough space, as the upgrade script creates backup of the db data.
* the afb_backup volume is for your safety, your data will be copied there.
* The script is assuming you have not changed the default db user and password.

##Troubleshooting
If you use your own postgresql image or changed any parameter, you have to manually migrate the data in docker volume afb_data to postgresql 10 format.
