## Application-specific tips and tricks
> :triangular_flag_on_post: **TODO**
* .NET in-process using Edge.js.
* [node-windows](https://github.com/coreybutler/node-windows): Windows services, logging, and commands using Node.js.

### Setting up and working with Azure DocumentDB

1. [Create a DocumentDB database account](https://azure.microsoft.com/en-us/documentation/articles/documentdb-create-account/)
2. [Create a database](https://azure.microsoft.com/en-us/documentation/articles/documentdb-create-database/)
3. [Create a collection](https://azure.microsoft.com/en-us/documentation/articles/documentdb-create-collection/)
4. [Add documents to the collection](https://azure.microsoft.com/en-us/documentation/articles/documentdb-view-json-document-explorer/)
5. Navigate to the root project directory and install the `documentdb` package: `npm install documentdb`
6. *(Optional, but helpful for IntelliSense support in Visual Studio Code)* Install the type definition file for DocumentDB with `tsd install documentdb`
7. Load the documentdb module: `var DocumentClient = require('documentdb').DocumentClient;`
8. Create a new `DocumentClient` object by specifying the endpoint URL and master key: `var ddbClient = new DocumentClient(endpointUrl, {masterKey: masterKey});`
 > :bulb: The endpoint URL and keys can be found in the Azure portal by navigating to your DocumentDB account
 
9. Query all documents in a particular collection in a database
```javascript
// note: the below code queries all documents in the collection with no 
// predicate to filter any documents out
ddbClient.queryDatabases('SELECT * from d WHERE d.id = "database_name"')
    .current(function (err, database) {
        ddbClient.queryCollections(database._self, 'SELECT * FROM c WHERE c.id = "collection_name"')
            .current(function (err, collection) {
                var docQuery = 'SELECT * FROM collection c';
                ddbClient.queryDocuments(collection._self, docQuery)
                    .toArray(function (err, documents) {
                        if (!err) {
                            console.log('found ' + documents.length + ' documents...');
                            for (var i = 0; i < documents.length; i++) {
                                console.log(documents[i]);
                            }
                        }
                    });
            });
    });
```

### Connecting to Microsoft SQL Server

* [tedious](https://www.npmjs.com/package/tedious) - TDS client written in JavaScript, no binary dependencies
* [mssql](https://www.npmjs.com/package/mssql) - Friendly interface wrapper around SQL clients, tedious by default.
* [mssql-ng](https://www.npmjs.com/package/mssql) - Next generation ES6-template interface for SQL (uses mssql/tedious).

### Setting up and working with MongoDB

1. [Install MongoDB on Windows](https://docs.mongodb.org/manual/tutorial/install-mongodb-on-windows/)
2. Install the MongoDB npm package in the project root by running `npm install mongodb`
3. *(Optional, but helpful for IntelliSense support in Visual Studio Code)* Install the type definition file for MongoDB with `tsd install mongodb`
4. Load the mongodb module: `var MongoClient = require('mongodb').MongoClient;`
5. [Determine your MongoDB connection string URI](https://docs.mongodb.org/manual/reference/connection-string/) and set it to a variable: `var mongoUrl = '...'`;
 > Example: mongodb://localhost:27017/yourDatabaseName

 > :bulb: MongoDB by default listens on 27017, but to verify this open the MongoDB log file `mongod.log` in the log directory and navigate the line that shows the port number (i.e. `[initandlisten] waiting for connections on port 27017`)
6. Access your MongoDB database by calling `MongoClient.connect()` and query the returned database
```javascript
MongoClient.connect(mongoUrl, function (err, db) {
    if (!err) {
        // query the collection and return a cursor to use
        // to access the data
        //
        // note: calling find() with no parameters is the equivalent
        // of pulling all documents in the collection with no
        // predicate
        var cursor = db.collection('yourCollectionName').find();

        // loop through all of the documents returned by the
        // query
        cursor.each(function (err, element) {
            if (!err && element) {
                // do something with the document
            }
            // if error and the document are undefined then
            // we have reached the no-more-documents condition
            if (!err && !element) {
                console.log('done!');
            }
        });
    }
});
```

### Azure Services

* [azure](https://www.npmjs.com/package/azure) - Full client for azure
* [azure-storage](https://www.npmjs.com/package/azure-storage) - client for Azure Storage services (Tables, Blobs, Files, Queues), which is part of the `azure` module above.
* [azure-storage-simple](https://www.npmjs.com/package/azure-storage-simple) - Promise based interface wrapper around `azure-storage` with a simpler UI.


## Accessing platform APIs
Sometimes you need to access platform functionality for which no suitable module is available. For example your app may need to access the registry running on a Windows Server or Desktop. In this case there are 2 ways to proceed. 

1. Create a native module add-on by wrapping code in C binding boilerplate code [using the V8 sdk and dev tools](https://nodejs.org/api/addons.html).
2. Use [ref](https://github.com/TooTallNate/ref) and [node-ffi](https://github.com/node-ffi/node-ffi) modules to access C buffers and call shared library (DLL) functions from javascript.

There are plenty of examples of [creating native modules](http://www.martinchristen.ch/node/tutorial11), including our notes on [Compiling native addon modules](windows-environment.md#compiling-native-addon-modules) but less on [using ref and node-ffi](http://opendirective.net/blog/2015/10/working-with-windows-native-code-from-node-js). [NPM module for Windows Registry](https://github.com/CatalystCode/windows-registry-node) contains examples of how it leveraged [node-ffi](https://www.npmjs.com/package/ffi), [ref](https://www.npmjs.com/package/ref),[ref-struct](https://www.npmjs.com/package/ref-struct), [Advapi32.dll](https://msdn.microsoft.com/en-us/library/windows/desktop/ms724875(v=vs.85).aspx), and [Shell32.dll](https://msdn.microsoft.com/en-us/library/windows/desktop/bb762154(v=vs.85).aspx) to enable Node.js applications to communicate with Windows interfaces.  

> :bulb: Note it is good practice to ensure published modules are written to run on all platforms (checkout writing cross platform modules and apps section in building-for-cross-platform.md), even though this can be considerable extra work. Modules that only work on Windows or Linux are likely to be unpopular so such code is best restricted to private modules or app code.
