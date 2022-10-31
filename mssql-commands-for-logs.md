
- `SELECT Name from sys.databases;`

Collecting the plan cache   
	- `select * from sys.dm_exec_cached_plans cross apply sys.dm_exec_sql_text(plan_handle);`   

Collect additional plan cache specifics   
	- `select * from sys.dm_exec_query_stats`   
	- `select * from sys.dm_exec_cached_plans cross apply sys.dm_exec_plan_attributes(plan_handle);`   
	- `Select * from ::fn_dblog(NULL, NULL);`   
