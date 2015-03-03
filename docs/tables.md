# Tables

Tantalim Tables are a 1 to 1 representation of tables in a relational database system such as MySQL, SQL Server, or Oracle.

```json
{
  "dbName": "db_column",
  "module": "Tables",
  "database": "Tantalim",
  "primaryKey": "ColumnID",
  "allowInsert": true,
  "allowUpdate": true,
  "allowDelete": true,
  "columns": [ARRAY_OF_COLUMNS],
  "joins": [ARRAY_OF_JOINS]
}
```

#### name

This is implied by the name of the file such as `Person.json`. Don't include this in the definition.

This name is the programmatic name for this table. It's used in join to clauses, SQL statements, and other programming statements.

#### dbName

Optional name of the table in the database. Defaults to the name of the table if left empty.

#### module

FUTURE USE: Modules provide a nice way to group tables. They aren't used any other way.

#### database

FUTURE USE: The name of the database the table is in.

#### primaryKey

The primary key or unique identifier of the table. This is required if you need to save data to the table. If it's read only, then you can skip this.

Note: Tantalim doesn't support composite primary keys at this time.

#### allowInsert

Optional Boolean true or false. Defaults to `true`.

#### allowUpdate

Optional Boolean true or false. Defaults to `true`.

#### allowDelete

Optional Boolean true or false. Defaults to `true`.


## Columns

Required list of columns for this table.

```json
{
  "name": "ColumnID",
  "dbName": "columnID",
  "dataType": "String",
  "label": "Column ID",
  "help": "Unique ID for this column",
  "placeholder": "Enter the unique ID",
  "fieldType": "text",
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

Optional name of the column in the database. Defaults to the column name if not specified.

#### dataType
Optional parameter that describes the type of column this represents. Defaults to `String` if not specified.
Refer to [Data Types](datatypes) for more information.

#### label
Optional default for [PageField.label](pages#fields). Defaults to the column name if not specified.

#### help
Optional default for [PageField.help](pages#fields)

#### placeholder
Optional default for [PageField.placeholder](pages#fields)

#### fieldType
Optional default for [PageField.fieldType](pages#fields). Defaults to `text` if not specified.

#### required

Optional Boolean value if the column is required. Defaults to `false`.

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
      "fromText": "XYZ",
      "to": "TableID"
    }
  ]
}
```

#### name

Programmatic name for this join. Required and unique to this table. Usually the same as table name.

#### table

The name of the target [table](tables#name) that this join points to.

#### required

Defaults to false. If true, then it uses an `INNER JOIN`, if false, then it uses a `LEFT JOIN`.

#### columns

* `from` is the name of the column in this table.
* `fromText` is the String that should be used to query from.
* `to` is the name of the column in the target table.

Examples:

* from: ChildParentID, to: PersonID
* from: IncludeCode, to: Code AND fromText: YesNo, to: LookupType
