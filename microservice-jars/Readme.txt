These jars are not built off of env variables.
The SQL connection, ports and secrets are hard coded.
Ensure you can connect to your MYSQL service with this information.

SQL connection information:
Host: localhost
Port: 3306
Database: alinedb (Create an empty database in your MYSQL service with this name.)
Username: root
Password: root

Run all services in seperate terminals and leave the terminals up while running them.
The services are running if they end with a line like this:
2022-02-24 19:37:54.906  INFO 12596 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8071 (http) with context path ''

If a service fails attempt to restart it.
Sometimes they do, sometimes they don't. This project is FUBAR.

Service start order and information.
Underwriter:
Start order: 1
Port: 8071
java -jar underwriter-microservice-0.1.0.jar
Endpoints: http://localhost:8071/applications

Bank:
Start order: 2
Port: 8083
Console command: 
java -jar bank-microservice-0.1.0.jar
Endpoints: Requires an authentication header of 'Bearer ' with a JWT token after Bearer.[
	http://localhost:8083/banks
	http://localhost:8083/branches
]

Transaction
Start order: 3
Port: 8073
Console command: java -jar transaction-microservice-0.1.0.jar
Endpoints: Requires an authentication header of 'Bearer ' with a JWT token after Bearer.
	http://localhost:8073/transactions

User:
Start order: 4
Port: 8070
Console command: java -jar user-microservice-0.1.0.jar
Endpoints:
	http://localhost:8070/users/registration
	http://localhost:8070/login 
Upon successful login it will send an authorization header back like this
Bearer eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ0ZXN0aW5nNCIsImF1dGhvcml0eSI6ImFkbWluaXN0cmF0b3IiLCJpYXQiOjE2NDU3NjA1NjAsImV4cCI6MTY0Njk3MDE2MH0.wSrEs2fAGa8j7l8nwBW5nhKHbpKWIjIbV0B4P35uRk4
