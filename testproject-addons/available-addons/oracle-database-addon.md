# Oracle Database Addon

This addon allows you to test connections and to send queries to Oracle databases. You can use this addon to send an SQL query and get the response in JSON format. Then, you can compare this output with the UI data.

### Available Actions

`Send SQL Query (Oracle Database)` - Send a SQL query to an Oracle Database

This action takes in the following input parameters:

* `Host` - Name of the host machine where the database is \(required\)
* `Port` - Port number to connect to \(default port is 3306 if none specified\)
* `Username` - Username to connect to the database \(required\)
* `Password` - Password for connecting to the database \(required\)
* `Query` - The SQL query you want to execute
* `SID` - System ID of the database you want to connect to \(default is None if it is not specified\)
* `Service` - Service name \(default is None if it is not specified\)

`Test SQL Connection (Oracle Database)` - Test the connection to the Oracle database

This action takes in the following input parameters:

* `Host` - Name of the host machine where the database is \(required\)
* `Port` - Port number to connect to \(default port is 3306 if none specified\)
* `Username` - Username to connect to the database \(required\)
* `Password` - Password for connecting to the database \(required\)
* `SID` - System ID of the database you want to connect to \(default is None if it is not specified\)
* `Service` - Service name \(default is None if it is not specified\)

