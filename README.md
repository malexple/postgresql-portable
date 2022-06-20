# postgresql-portable
How to run postgresql without installation

1. To get started, you need the server binaries for Windows. You can either copy the PostgreSQL folder (minus the data folder) from an existing server installation, or simply download the files from the [PostgreSQL](https://www.postgresql.org/download/windows/) Windows section of the site. Make sure the .zip archive is selected. 

3. Next, copy the following batch file to the root of the new PostgreSQL folder.

4. On first use, uncomment the line in the initdb call.

5. Run the batch file.

Below is a script that starts the PostgreSQL server and, on pressing the Enter key, stops the service. We use this script as part of a standalone development and testing kit running PostgreSQL 9.0-beta. We're running the process on a non-standard port (5439 so we know it's a 9.0 server). To initialize the database for the first time, you will need to run the initdb command. You only need to initialize the database once. Next, you can transfer the folder to a USB device if you wish. The %CD% variable returns the path to the folder where the batch file is located.

```
@ECHO ON
REM Setting environment variables to run PostgreSQL
@SET PATH="%CD%\bin";%PATH%
@SET PGDATA=%CD%\data
@SET PGDATABASE=postgres
@SET PGUSER=postgres
@SET PGPORT=5439
@SET PGLOCALEDIR=%CD%\share\locale
REM %CD%\bin\initdb -U postgres -A trust
%CD%\bin\pg_ctl -D %CD%/data -l logfile start
ECHO "Press Enter to stop the server"
pause
%CD%\bin\pg_ctl -D %CD%/data stop
```


