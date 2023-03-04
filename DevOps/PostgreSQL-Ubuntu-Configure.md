# Setting up PostgreSQL Database on Ubuntu 16+ servers

This readme file describes how to install and set up PostgreSQL on Ubuntu 16+ servers.


## Tech and Pre-requisites

- [Ubuntu 16+ server] - A running Ubuntu Xenial and above server running on cloud or on-premise.

### PostgreSQL
PostgreSQL is a powerful and open-source relational database management system (RDBMS) that is designed to be highly scalable, secure, and extensible. It is widely used in enterprise applications and is considered one of the most advanced and feature-rich database systems available today. PostgreSQL supports a wide range of data types, including text, numeric, date and time, and spatial data, and provides support for advanced features such as transactions, stored procedures, triggers, and views. It is also highly customizable, with support for user-defined functions and custom extensions that can be used to extend its functionality.

One of the key advantages of PostgreSQL is its strong emphasis on data integrity and security. It provides support for various authentication methods, including SSL encryption, and also provides fine-grained access controls that can be used to limit access to sensitive data. PostgreSQL also offers a high level of scalability, with support for horizontal scaling through sharding and replication. It can handle very large datasets and can support thousands of concurrent connections, making it ideal for high-traffic applications.

Overall, PostgreSQL is a robust and reliable database system that offers a wide range of advanced features and strong data security measures. Its open-source nature and active community make it a popular choice for businesses and organizations of all sizes.
### Installing and configuring PostgreSQL database

Create a React App using below command, *my-app* is the name of the App. This step is going to take some time to install all the dependencies that react requires. Instead of *npx*, you can use *npm* or *yarn* as well to set up a reactJS application(refer to documentation listed above).
```sh
sudo apt update
sudo apt install postgresql postgresql-contrib curl
```
Lets hop into postgreSQL using below command, postgres is a default user provided by default
```sh
sudo -u postgres psql
```
Create database
```sh
create database <db_name>;
```
Create user and assign a password
```sh
create user <user_name> with password '<password>';
```
Set encoding to utf-8, although PostgreSQL use default encoding as utf-8, it is important to set this in the case if default encoding changes
```sh
alter role <user_name> set client_encoding to 'utf8';
```
Set transaction isolation
```sh
alter role <user_name> set default_transaction_isolation to 'read committed';
```
Set timezone to UTC
```sh
alter role <user_name> set timezone to 'UTC';
```
Below command gives admin access to user on the database
```sh
grant all privileges on database <db_name> to <user_name>;
```

## License

**Free Software, Hell Yeah!**
