# Models

## Model Definition

```json
{
  "basisTable": "TableName",
  "limit": 10,
  "orderBy": [ARRAY_OF_ORDER_CLAUSES],
  "fields": [ARRAY_OF_FIELD_DEFINITIONS],
  "steps": [ARRAY_OF_STEPS],
  "children": [ARRAY_OF_MODEL_DEFINITONS]
}
```

#### basisTable

Tantalim data architecture is based on a simple concept that joins always travel from many-to-one or one-to-one unless
incorporating a child set of records (one-to-many). The basis table (or tables in the case of a multi-view model) keeps
all the data in the view together. All other fields should be reachable from a M:1 or 1:1 join.

#### limit

The default limit of records that can be retrieved without paging. In general, models with a lot of fields should use a
smaller limit. "Thin" models with no children and just a few fields can have a very high limit.

#### orderBy

The default order by clause if one is not supplied.

```json
{
  "fieldName": "TableName",
  "direction": "ASC"
}
```
Above is a typical order by clause.

* `fieldName` is the programmatic field as listed in this model.
* `direction` is the sort order such as ASC (default) or DESC.

#### children

One of the most powerful features of Tantalim is the ability to combine multiple views of related data into a single
set of pages. `children` is an array of model views that are related to the parent model in a one-to-many
(parent-to-child) relationship.

## Steps

Steps define the pathway from one table to the next on a query. They rely on previously defined Table Joins.

```json
    {
      "name": "FromTableToModule",
      "previousStep": "FromTableToDatabase", // optional
      "required": false,                     // optional
      "join": "ToModule"
    },
```

## Fields

```json
{
  "name": "TableJoinToTableName",
  "step": "302",
  "basisColumn": "Name"
  "dataType": "String",
  "fieldDefault": {
    "type": "field",
    "value": "TableName",
    "updateable": false
  }
}
```

#### name
Required name of the field. Used as programmatic identifier of field (can be used as object properties and JavaScript).
Should follow standard naming conventions for variables. Typically, the field should be `StepName` + `TableColumnName`.

#### step
Identifies which table this field belongs. Defaults to the basis table if not included.

#### basisColumn
JSON for the table column this field references. `dbName` is expected. Some fields may not reference a database column.
In these cases, a function may be expected.

#### dataType
Optional parameter that describes the type of column this represents. If not specified, it should (probably??) use the
`basisColumn.dataType` value.

* TODO - list out the valid data types
* Boolean

#### fieldDefault
Optional parameter that describes any default values when inserting a new instance into the set.

##### fieldDefault.type
The type of default.

* constant (default if not specified) - any constant default value such as 1 or HelloWorld
* sourceField - any value from a field in the current instance or in a parent instance, such as TableID
* fxn - any JavaScript function to be executed, such as "function() { return 1 + 1 }"

##### fieldDefault.value
The constant value, source field name, or function text.

##### fieldDefault.updateable
When `type` equals "field", updateable means that the value will keep defaulting everytime the source field changes.
