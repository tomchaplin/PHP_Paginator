# Paginator

## About
PHP_Pagiantor is a basic class for PHP which enables easy pagination of data retrieved from a database, using PDO prepared statements.

### Features
* Database queries through PDO prepared statements to protect against SQL injection attacks
* Compatability with MySQL, H2, HSQLDB, Postgres, and SQLite ([due to use of LIMIT, OFFSET clause](https://stackoverflow.com/a/24046664))
* Navigation customisable though user-specified class names
* Ability to change number of results per page
* Object-oriented approach

## Usage

## To-do
* Add support for more databases
* Add exceptions
* Better string handling
