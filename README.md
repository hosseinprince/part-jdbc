JDBC API Wrapper for node.js
===================

Latest Version   0.3.3
-------------

Installation
-------------
Release: npm i --save part-jdbc

نحوه ی استفاده :
-------------------
//in config.js
```
var jinst = require('jdbc/lib/jinst');
if (!jinst.isJvmCreated()) {
    jinst.addOption("-Xrs");
    jinst.setupClasspath(['./ojdbc7.jar']);
}
exports.JDBCConfig = {
    // Required
    url: 'exampleUrl',
    properties: {
        user: user db,
        password: 'pass db'
        // Other driver supported properties can be added here as well.
    }
};
```


----------
  Query the database. 
-------------

  Select statement with auto commit. 
-------------
```
 openConn(config.JDBCConfig)
        .then(function (jdbc) {
		   var query = "select name , userName , password from myTable";		  
           queryResult(jdbc, query )
                .then(function (result) {
                   console.log(result);
                })
                .fail(function (error) {
                console.log("error in result:",error);
             
                })
                .done(function () {
                 
                });
        })
        .fail(function (error) {
            console.log("error in OpenConn:",error);
        });
```

  Select statement with manual commit. 
-------------
```
 openConn(config.JDBCConfig, false)
        .then(function (jdbc) {
		   var query = "select name , userName , password from myTable";
           queryResult(jdbc, query )
                .then(function (result) {
                   console.log(result);
                })
                .fail(function (error) {
                console.log("error in result:",error);
               
                })
                .done(function () {
                
                });
        })
        .fail(function (error) {
            console.log("error in OpenConn:",error);
        });
```
----------
Update statement
--------------------

```
openConn(config.JDBCConfig)
        .then(function (jdbc) {
         var query =
          "update myTable set name = 'vahid' , password = '123456'";
            queryResultUpdate(jdbc, query)
                .then(function (count) {
                //count: number of updated rows
                   console.log(count);
                })
                .fail(function (error) {
                console.log("error in result:",error);
                 closeConn(jdbc,config.JDBCConfig);
                })
                .done(function () {
                    closeConn(jdbc,config.JDBCConfig);
                });
        })
        .fail(function (error) {
            console.log("error in OpenConn:",error);
        });
```
----------
reqular insert statement 
--------------------

```
openConn(config.JDBCConfig)
        .then(function (jdbc) {
         var query =
          "insert into myTable (name , password) VALUES ('vahid','123456')";
          var getGeneratedKeys = false;
            queryResultInsert(jdbc, query , getGeneratedKeys )
                .then(function (count) {
                //count:number of row inserted
                   console.log(count);
                })
                .fail(function (error) {
                console.log("error in result:",error);
                 closeConn(jdbc,config.JDBCConfig);
                })
                .done(function () {
                    closeConn(jdbc,config.JDBCConfig);
                });
        })
        .fail(function (error) {
            console.log("error in OpenConn:",error);
        });

```

----------
Insert statement with generated Keys
--------------------

```
openConn(config.JDBCConfig)
        .then(function (jdbc) {
         var query =
          "insert into myTable (name , password) VALUES ('vahid','123456')";
          var getGeneratedKeys = true;
            queryResultInsert(jdbc, query , getGeneratedKeys )
                .then(function (data) {
                   console.log(data);
                   /*
						console.log output:
						{count: count, rowId: rowIdHash}
					*/
                })
                .fail(function (error) {
                console.log("error in result:",error);
                 closeConn(jdbc,config.JDBCConfig);
                })
                .done(function () {
                   
                });
        })
        .fail(function (error) {
            console.log("error in OpenConn:",error);
        });

```
### Table of contents

You can insert a table of contents using the marker `[TOC]`:

[TOC]

