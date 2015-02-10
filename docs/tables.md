# Tables

Tantalim Tables are a 1 to 1 representation of tables in a relational database system such as MySQL, SQL Server, or Oracle.

```json
{
  "dbName": "db_column",
  "primaryKey": "ColumnID",
  "columns": [ARRAY_OF_COLUMNS],
  "joins": [ARRAY_OF_JOINS]
}
```

#### dbName

The name of the table in the database.

#### primaryKey

The primary key or unique identifier of the table. Tantalim doesn't support composite primary keys at this time.

## Columns
```json
{
  "name": "ColumnID",
  "dbName": "columnID",
  "dataType": "String",
  "required": true,
  "updateable": false,
  "columnDefault": "GUID"
}
```

#### name
Programmatic name of the column. This is used in the following places:

* Table - primaryKey
* Table - Joins - columns - from
* Table - Joins - columns - to
* Model - Fields - basisColumn

#### dbName

The name of the column in the database.

#### dataType
Optional parameter that describes the type of column this represents. Defaults to String if not specified.
Refer to [Data Types](datatypes) for more information.

#### required

Optional, Boolean value if the column is required. Defaults to `false`.

#### updateable

Optional Boolean value if the column can be changed. Defaults to `true`.

#### columnDefault

When created, should the column get a default value.

* Autoincrement
* GUID
* CreatedDate - current time of database on insert
* UpdatedDate - current time of database on insert or update
* CreatedByUserID
* CreatedByUsername
* UpdatedByUserID
* UpdatedByUsername
* UpdatedByProcess

## Joins

```json
{
  "name": "Table",
  "table": "Table",
  "required": true,
  "columns": [
    {
      "from": "TableID",
      "to": "TableID"
    }
  ]
}
```

#### required

Defaults to false. If true, then it uses an inner join, if false, then left join.

#### columns

`from` is the name of the column in this table. `to` is the name of the column in the target table.
