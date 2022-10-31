# mssql-docker-forensics-mdf-ldf
Reading mdf and ldf files from a forenscis image

Make sure password is complex otherwise it will not remain running. 
```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=yourStrong===Password" -p 1433:1433 -v mssql:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-latest
```
Add mdf and ldf files to /mssql/data/.   
Change the container name if required 
```bash
docker cp /mssql/data/database_file.mdf <container_name>:/var/opt/mssql/data/
docker cp /mssql/data/database_file_log.ldf <container_name>:/var/opt/mssql/data/
```
Connect to container and use sqlcmd   
add `-o output.txt` for easier output. NOTE: will not display in terminal.
```bash
docker exec -it "<container_name>" /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P "yourStrong===Password"
```
Create database   
Add the mdf and ldf files    
```sql
use master;
GO
create database database_file ON
( FILENAME = N'/var/opt/mssql/data/database_file.mdf' ),
( FILENAME = N'/var/opt/mssql/data/database_file_log.ldf' )
for attach
GO
use database_file;
GO
```
