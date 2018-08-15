# Paginator

## About
Pagiantor is a basic class for PHP which enables easy pagination of data retrieved from a database, using PDO prepared statements.

### Features
* Database queries through PDO prepared statements to protect against SQL injection attacks
* Compatability with MySQL, H2, HSQLDB, Postgres, and SQLite ([due to use of LIMIT, OFFSET clause](https://stackoverflow.com/a/24046664))
* Navigation customisable though user-specified class names
* Ability to change number of results per page
* Object-oriented approach

## Usage

Note, it is advisable to have a working knowledge of PDOs and PDOStatements before using this class. For more information on these objects please consult the [PHP manual](http://php.net/manual/en/book.pdo.php). To explain the usage we will run through an example where we wish to paginate data from a table called `articles` which has columns `id`, `title` and `author`. Throughout this example we will assume that `$pdo` is a valid PDO object connected to the database containing this table.

### Setup a new Paginator
Before we can use the class we need to include the class file. Download the class file, place it somewhere in the file structure of your project and include it at the top of the PHP file upon which you wish to display the paginated data. 

```php
include_once "path_to/Pagiantion.class.php";
```
Next we will construct a new Paginator object. The constructor function requires 3 inputs:
1. A PDO object which should be connected to your database,
2. The query returning the data you wish to paginate,
3. The total number of rows this query will return.

Optionally, the user may also provide a callback function. This function should accept a PDO object and should bind any parameters in your query.

```php
$query = "SELECT * FROM articles WHERE author LIKE :author";

// Callback function which will bind $_GET['author'] to the :author parameter
function bind_my_params($stmt) {
  $stmt->bindValue(':author',$_GET['author']);
}

// Now we figure out how many rows to expect
$count_query = "SELECT COUNT(*) FROM articles WHERE author LIKE :author";
$count_stmt = $pdo->prepare($count_query);
bind_my_params($count_stmt);
$count_stmt->execute();
$total_rows = $stmt->fetch()['COUNT(*)'];

// Finally we set up our Paginator
$paginator = new Paginator($pdo,$query,$total_rows,'bind_my_prams');
```

### Update the page
To update the page we must tell the paginator which page we are on and how many results we are displaying per page. These values will be `$_GET['page']` and `$_GET['limit']` respectively. In case we have arrived on the page without these values specified in the query we must set some defaults.

```php
  // We default to page 1, displaying 5 results
  $page = (empty($_GET['page'])) ? 1 : $_GET['page'];
  $limit = (empty($_GET['limit'])) ? 5 : $_GET['limit'];
  // Now we update these values in the Paginator
  $paginator->updatePage($page,$limit);
```

### Retreive rows
### Setup navigation
### Setup 'results per page' buttons

## To-do
* Automatically detect total number of rows from base query
* Add support for more databases
* Add exceptions
* Better string handling

## References
* https://code.tutsplus.com/tutorials/how-to-paginate-data-with-php--net-2928
