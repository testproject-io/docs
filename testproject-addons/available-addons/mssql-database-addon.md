# MSSQL Database Addon

This addon allows you to test the connection and to send a query to MSSQL databases. You can use this addon to send an SQL query and get the response in JSON format. Then, you can compare this output with the UI data.

### Available Actions

`Send SQL Query (MSSQL)` - Run Send SQL Query \(MSSQL\)

This action takes in the following input parameters:

* `Host` - Name of the host machine where the database is \(required\)
* `Port` - Port number to connect to \(Default port is 1433 if none specified\)
* `Username` - Username to connect to the database \(required\)
* `Password` - Password for connecting to the database \(required\)
* `DbName` - Name of the database you are connecting to \(required\)
* `Query` - The SQL query you want to execute

`Test SQL Connection (MSSQL)` - Run a test to ensure that the SQL connection \(MSSQL\) is working

This action takes in the following input parameters:

* `Host` - Name of the host machine where the database is \(required\)
* `Port` - Port number to connect to \(Default port is 1433 if none specified\)
* `Username` - Username to connect to the database \(required\)
* `Password` - Password for connecting to the database \(required\)
* `DbName` - Name of the database you are connecting to \(required\)



