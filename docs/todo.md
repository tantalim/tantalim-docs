# TODO

## Up Next

### Enable selects with where clauses
[Example](http://localhost:3000/page/BuildTable/#/p/TableJoins)
From Column

## Later

### Add Support for Transactions

[Using Knex Transactions](http://knexjs.org/#Transactions)

### Setup Code Coverage

Add https://coveralls.io/

* https://coveralls.io/r/tantalim/tantalim-client
* https://coveralls.io/r/tantalim/tantalim-server

### Allow selects with only a few values
[Example](http://localhost:3000/page/BuildTable/#/p/TableJoins)

* OM -> One to Many
* MM -> Many to Many

Three types of select:

* static - for just a few records with constant values that are the same everytime the page is views. Examples: Yes/No, Countries
* dynamic - for fewer than 1000 records, support client side filtering and dependent where clauses. Examples: Employees in a small company, Columns in a table.
* infinite - for more than 1000 possible records, support server side filtering and paging. Examples: Github Projects, Wikipedia articles

### Add error message handling
Show queue of messages. Use a directive.
tantalim-errors.info/warn/error
choose which errors I want to see

### Support copy and paste to/from multiple view
to and from Excel
http://stackoverflow.com/questions/21028578/how-to-get-clipboard-data-in-angular-js

### Improve the key binding for changing instances
* know when user is focused on the quick nav or multiple view
* know which view should be changed
