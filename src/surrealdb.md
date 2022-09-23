# Surreal DB: new Relation, Document, schemaless / Schemaful DB

- First lets install Surreal DB

## Installation

### MacOS

```sh
brew install surrealdb/tap/surreal
```

### Windows

```sh
iwr https://windows.surrealdb.com -useb | iex

# Alternatively SurrealDB is available for installation, on Windows, via the Chocolatey package
choco install surreal --pre

# Using Chocolatey, SurrealDB can be upgraded to the latest version with the following command.
choco upgrade surreal --pre
```

### Linux

```sh
curl -sSf https://install.surrealdb.com | sh
```

### Run using Docker

```sh
docker run --rm -p 8000:8000 surrealdb/surrealdb:latest start
```

- I tried using the docker install first but that seems to only store data in memory. I'm sure there is a way to persist the data by specifying a data directory outside of the container, but not knowing the folder structure of surreal yet, makes that a bit difficult at the moment.
- So I'm going to install SurrealDB with the `curl` method for Linux and see what happens next


##  Using the JS Library

First install the JavaScript NPM package

```sh
npm install --save surrealdb.js
```

Or use Yarn

```sh
yarn add surrealdb.js
```

I've been making a point of using NPM for all global installs and using Yarn for all my project only installs, but that is just personal preference.

## Connect to SurrealDB

Create a new app.js file and add the following code to try out some basic operations using the SurrealDB driver.

```js
import Surreal from 'surrealdb.js';

const db = new Surreal('http://127.0.0.1:8000/rpc');

async function main() {

	try {

		// Signin to a scope from the browser
		await db.signin({
			NS: 'test',
			DB: 'test',
			SC: 'user',
			user: 'info@surrealdb.com',
			pass: 'my-secret-password',
		});

		// Select a specific namespace / database
		await db.use('test', 'test');

		// Create a new person with a random id
		let created = await db.create("person", {
			title: 'Founder & CEO',
			name: {
				first: 'Tobie',
				last: 'Morgan Hitchcock',
			},
			marketing: true,
			identifier: Math.random().toString(36).substr(2, 10),
		});

		// Update a person record with a specific id
		let updated = await db.change("person:jaime", {
			marketing: true,
		});

		// Select all people records
		let people = await db.select("person");

		// Perform a custom advanced query
		let groups = await db.query('SELECT marketing, count() FROM type::table($tb) GROUP BY marketing', {
			tb: 'person',
		});

	} catch (e) {

		console.error('ERROR', e);

	}

}

main();
```

Now you can run the app by entering the following in your terminal

```sh
node app.js
```

## Methods that's part of the Library


| Function	                  | Description                                                                     |
|-----------------------------|---------------------------------------------------------------------------------|
| Surreal.InstanceS  `STATIC` | Connects to a specific database endpoint                                        |
| db.connect(url)	          | Connects to a local or remote database endpoint                                 |
| db.wait()	                  | Waits for the connection to the database to succeed                             |
| db.close()	              | Closes the persistent connection to the database                                |
| db.use(ns, db)	          | Switch to a specific namespace and database                                     |
| db.signup(vars)	          | Signs this connection up to a specific authentication scope                     |
| db.signin(vars)	          | Signs this connection in to a specific authentication scope                     |
| db.invalidate()	          | Invalidates the authentication for the current connection                       |
| db.authenticate(token)	  | Authenticates the current connection with a JWT token                           |
| db.let(key, val)	          | Assigns a value as a parameter for this connection                              |
| db.query(sql, vars)	      | Runs a set of SurrealQL statements against the database                         |
| db.select(thing)	          | Selects all records in a table, or a specific record                            |
| db.create(thing, data)	  | Creates a record in the database                                                |
| db.update(thing, data)	  | Updates all records in a table, or a specific record                            |
| db.change(thing, data)	  | Modifies all records in a table, or a specific record                           |
| db.modify(thing, data)	  | Applies JSON Patch changes to all records in a table, or a specific record      |
| db.delete(thing)	          | Deletes all records, or a specific record                                       |


## Surreal.Instance

The `Instance` static singleton ensures that a single database instance is available across very large or complicated applications. With the singleton, only one connection to the database is instantiated, and the database connection does not have to be shared across components or controllers.

```js
const Surreal = require('surrealdb.js');

async function main() {
	try {
		// Connect to the database
		await Surreal.Instance.connect('https://cloud.surrealdb.com/rpc');
		// Select a namespace + database
		await Surreal.Instance.use("test", "test");
		// Create or update a specific record
		await Surreal.Instance.update("person:tobie", {
			name: 'Tobie',
		});
	} catch (e) {
		console.error('ERROR', e);
	}
}

main();
```

## db.connect(url)

Connects to a local or remote database endpoint.

| Arguments         | Description                                       |
|-------------------|---------------------------------------------------|
| url  `REQUIRED`	| The url of the database endpoint to connect to.   |

```js
// Connect to a local endpoint
await db.connect('http://127.0.0.1:8000/rpc');
// Connect to a remote endpoint
await db.connect('https://cloud.surrealdb.com/rpc');
```

## db.wait()

Waits for the connection to the database to succeed.

```js
await db.wait();
```

## db.close()

Closes the persistent connection to the database.

```js
db.close();
```

## db.use(ns, db)

Switch to a specific namespace and database.

| Arguments	     | Description                          |
|----------------|--------------------------------------|
| ns  `REQUIRED` | Switches to a specific namespace.    |
|db  `REQUIRED`	 | Switches to a specific database.     |

```js
await db.use('test', 'test');
```

## db.signup(vars)

Signs up to a specific authentication scope

| Arguments        | Description                        |
|------------------|------------------------------------|
| vars  `REQUIRED` | Variables used in a signup query.  |

```js
let token = await db.signup({
	NS: 'test',
	DB: 'test',
	SC: 'user',
	email: 'info@surrealdb.com',
	pass: '123456',
});
```

## db.signin(vars)

Signs in to a specific authentication scope.

| Arguments	        | Description                       |
|-------------------|-----------------------------------|
| vars  `REQUIRED`	| Variables used in a sign in query. |

```js
let token = await db.signin({
	NS: 'test',
	DB: 'test',
	SC: 'user',
	email: 'info@surrealdb.com',
	pass: '123456',
});
```

## db.invalidate()

Invalidates the authentication for the current connection.

```js
await db.invalidate();
```

## db.authenticate(token)

Authenticates the current connection with a JWT token.


| Arguments	        | Description                   |
|-------------------|-------------------------------|
| token  `REQUIRED`	| The JWT authentication token. |

```js
await db.authenticate('eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJTdXJyZWFsREIiLCJpYXQiOjE1MTYyMzkwMjIsIm5iZiI6MTUxNjIzOTAyMiwiZXhwIjoxODM2NDM5MDIyLCJOUyI6InRlc3QiLCJEQiI6InRlc3QiLCJTQyI6InVzZXIiLCJJRCI6InVzZXI6dG9iaWUifQ.N22Gp9ze0rdR06McGj1G-h2vu6a6n9IVqUbMFJlOxxA');
```

## db.let(key, val)

Assigns a value as a parameter for this connection.

| Arguments	      | Description                             |
|-----------------|-----------------------------------------|
| key  `REQUIRED` |	Specifies the name of the variable.     |
| val  `REQUIRED` |	Assigns the value to the variable name. |

```js
// Assign the variable on the connection
await db.let('name', {
	first: 'Tobie',
	last: 'Morgan Hitchcock',
});
// Use the variable in a subsequent query
await db.query('CREATE person SET name = $name');
// Use the variable in a subsequent query
await db.query('SELECT * FROM person WHERE name.first = $name.first');
```

## db.query(sql, vars)

Runs a set of SurrealQL statements against the database.


| Arguments       | Description                                           |
|-----------------|-------------------------------------------------------|
| sql  `REQUIRED` |	Specifies the SurrealQL statements.                   |
| vars `OPTIONAL` |	Assigns variables which can be used in the query.     |

```js
// Assign the variable on the connection
let result = await db.query('CREATE person; SELECT * FROM type::table($tb);', {
	tb: 'person',
});
// Get the first result from the first query
let created = result[0].result[0];
// Get all of the results from the second query
let people = result[1].result;
```

## db.select(thing)

Selects all records in a table, or a specific record, from the database.

| Arguments        | Description                              |
|------------------|------------------------------------------|
| thing `REQUIRED` | The table name or a record ID to select. |

```js
// Select all records from a table
let people = await db.select('person');
// Select a specific record from a table
let person = await db.select('person:h5wxrf2ewk8xjxosxtyc');
```

This function will run the following query in the database:

```js
SELECT * FROM $thing;
```

## db.create(thing, data)

Creates a record in the database.

| Arguments      	| Description                                         |
|-------------------|-----------------------------------------------------|
| thing  `REQUIRED`	| The table name or the specific record ID to create. |
| data  `OPTIONAL`	| The document / record data to insert.               |

```js
// Create a record with a random ID
let person = await db.create('person');
// Create a record with a specific ID
let record = await db.create('person:tobie', {
	name: 'Tobie',
	settings: {
		active: true,
		marketing: true,
	},
});
```

This function will run the following query in the database:

```js
CREATE $thing CONTENT $data;
```

## db.update(thing, data)

Updates all records in a table, or a specific record, in the database.

> This function replaces the current document / record data with the specified data.


| Arguments         | Description                                           |
|-------------------|-------------------------------------------------------|
| thing  `REQUIRED` |	The table name or the specific record ID to update. |
| data   `OPTIONAL` |	The document / record data to insert.               |

```js
// Update all records in a table
let people = await db.update('person');
// Update a record with a specific ID
let person = await db.update('person:tobie', {
	name: 'Tobie',
	settings: {
		active: true,
		marketing: true,
	},
});
```

This function will run the following query in the database:

```js
UPDATE $thing CONTENT $data;
```

## db.change(thing, data)

Modifies all records in a table, or a specific record, in the database.

> This function merges the current document / record data with the specified data.

| Arguments	        | Description                                         |
|-------------------|-----------------------------------------------------|
| thing  `REQUIRED`	| The table name or the specific record ID to change  |
| data  `OPTIONAL`	| The document / record data to insert.               |

```js
// Update all records in a table
let people = await db.change('person', {
	updated_at: new Date(),
});
// Update a record with a specific ID
let person = await db.change('person:tobie', {
	updated_at: new Date(),
	settings: {
		active: true,
	},
});
```

This function will run the following query in the database:

```js
UPDATE $thing MERGE $data;
```

## db.modify(thing, data)

Applies JSON Patch changes to all records, or a specific record, in the database.

> This function patches the current document / record data with the specified JSON Patch data.

| Arguments	        | Description                                           |
|-------------------|-------------------------------------------------------|
| thing  `REQUIRED`	| The table name or the specific record ID to modify.   |
| data  `OPTIONAL`	| The JSON Patch data with which to modify the records. |

```js
// Update all records in a table
let people = await db.modify('person', [
	{ op: "replace", path: "/created_at", value: new Date() },
]);
// Update a record with a specific ID
let person = await db.modify('person:tobie', [
	{ op: "replace", path: "/settings/active", value: false },
	{ op: "add", "path": "/tags", "value": ["developer", "engineer"] },
	{ op: "remove", "path": "/temp" },
]);
```

This function will run the following query in the database:

```js
UPDATE $thing PATCH $data;
```

## db.delete(thing)

Deletes all records in a table, or a specific record, from the database.

| Arguments	         | Description                              |
|--------------------|------------------------------------------|
| thing  `REQUIRED`  | The table name or a record ID to select. |

```js
// Delete all records from a table
await db.delete('person');
// Delete a specific record from a table
await db.delete('person:h5wxrf2ewk8xjxosxtyc');
```

This function will run the following query in the database:

```js
DELETE * FROM $thing;
```