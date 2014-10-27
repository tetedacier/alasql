alasql.js - javascript SQL-database - version 0.0.1
===

Sorry, work still in progress. All features below are still do not work.

* * *

Alasql - this is lightweight client-side SQL database designed to work in browser and Node.js. 

Installation
===
In browser - just save file [alasql.js](./src/alasql.js).

In Node.js use the following command:

  npm install alasql

In browser
==
```
  test.html
  =========
  <script src="sql-parser.js"></script>
  <script src="alasql.js"></script>	
  <script>
    var db = new alasql.Database();
    db.run("CREATE TABLE test (one INT, two NVARCHAR(MAX))");
    db.run("INSERT INTO test (1,2)");
    db.tables.test.recs.push({one:3,two:4});
    console.table(db.exec("SELECT * FROM test"));
  </script>

```
In Node.js
==
```
    var alasql = require('alasql.js');
    var db = new alasql.Database();
    db.run("CREATE TABLE test (one INT, two NVARCHAR(MAX))");
    db.tables.test.recs = \[
        {one:3,two:4},
        {one:5,two:6},
    \];
    var res = db.exec("SELECT * FROM test ORDER BY two DESC");
    console.log(res[0].one);

```

Supported SQL statements
==
* SELECT FROM JOIN ON WHERE GROUP BY HAVING ORDER BY LIMIT
* INSERT INTO table \[ (field1, field2) \] VALUES (value1, value2)
* UPDATE table SET field = value1, field = value2 WHERE condition
* DELETE FROM table WHERE condition
* CREATE TABLE \[IF NOT EXIST\] table
* DROP TABLE \[IF EXIST\] table
* ALTER TABLE table1 RENAME TO table2


SELECT statement
==

Now alasql supports following subset of SELECT syntax:

* SELECT field1, field2 AS alias3, FUNCTION(field4+field5) AS alias6, SUM(field7) AS alias8, *, table2.*
* FROM table1
* LEFT/INNER JOIN table2 ON condition
* WHERE condition
* GROUP BY field1, alias3
* HAVING condition
* ORDER BY field1, alias3
* LIMIT number

FUNCTIONS
==
* ABS
* MIN
* MAX

AGGREGATORS
==
* SUM()
* COUNT 

Database methods
==

Each database can be used with the following sync methods:

* new Database() - create new alasql-database
* .run(sql-statment) - run
* .exec(sql-statement) - executes SELECT query and returns array of objects 


Prerequisites
==
[sql-parser.js](https://github.com/forward/sql-parser) - SQL Parser by Andrew Kent

Performance
===

Limitations
==

Tests
==

I use mocha for tests. Just run incommand line:

```
  mocha
```


Credits
==
Many thanks to Andrew Kent for his SQL Parser and other people for other useful tools, which made our work much easier.

License
==

(c) 2014, Andrey Gershun (agershun@gmail.com), [MIT licance information](LICENSE)

