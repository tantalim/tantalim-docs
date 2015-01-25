# Models

## Model Definition

```json
{
  "data": {
    "modelName": "BuildTable"
  },
  "basisTable": TABLE_DEFINITION,
  "primaryKey": FIELD_DEFINITION,
  "limit": 10,
  "orderBy": [ARRAY_OF_ORDER_CLAUSES],
  "fields": [ARRAY_OF_FIELD_DEFINITIONS],
  "steps": [ARRAY_OF_STEPS],
  "children": [ARRAY_OF_MODEL_DEFINITONS]
}
```

#### data.modelName

The unique programmatic name for this model.
TODO: figure out if and when we'll need to consider the "package" or application module this model is in. Hopefully, we
can do it like most programming languages, ie. assume the modelName refers to a model in this module or application or
list the module along with the modelName.

#### basisTable

Tantalim data architecture is based on a simple concept that joins always travel from many-to-one or one-to-one unless
incorporating a child set of records (one-to-many). The basis table (or tables in the case of a multi-view model) keeps
all the data in the view together. All other fields should be reachable from a M:1 or 1:1 join.

```json
{
  "dbName": "db_table",
  "primaryKey": {
    "columnName": "TableID",
    "dbName": "tableID"
  }
}
```
Above is a standard (if not minimalistic) table definition.

#### primaryKey

This instance's (row's) unique identifier. See [Field Definition](#field-definition) for more details.
TODO: consider renaming this to instanceID or something else so it's not confused with `basisTable.primaryKey`.

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

#### fields

#### steps

#### children

One of the most powerful features of Tantalim is the ability to combine multiple views of related data into a single
set of pages. `children` is an array of model views that are related to the parent model in a one-to-many
(parent-to-child) relationship.

## Model Step Definition

```json
    {
      "stepStepID": "100",
      "stepPreviousStepID": null,
      "joinToTableSql": "app_module",
      "joinRequired": "0",
      "joinColumns": [
        {
          "fromColSql": "moduleID",
          "fromText": null,
          "toColSql": "moduleID"
        }
      ],
      "stepCount": 1
    }
```

## Model Field Definition

```json
{
  "fieldName": "TableJoinToTableName",
  "fieldStepID": "302",
  "basisColumn": {
    "dbName": "name"
  }
}
```

#### fieldName
Required name of the field. Used as programmatic identifier of field (can be used as object properties and JavaScript).
Should follow standard naming conventions for variables. Typically, the field should be `StepName` + `TableColumnName`.

#### fieldStepID
Identifies which table this field belongs. Defaults to the basis table if not included.

#### basisColumn
JSON for the table column this field references. `dbName` is expected. Some fields may not reference a database column.
In these cases, a function may be expected.

## Data

```json
[
  {
    "id": "1",
    "data": [OBJECT_DATA],
    "children": {
      "[STEP_NAME]": [
        {
          "id": "11",
          "data": [OBJECT_DATA],
          "foreignKey": "1"
        }
      ]
    }
  }
]
```

#### id

TODO

#### data

TODO

```json
{
  "EmployeePersonID": "1",
  "EmployeePersonName": "John Doe",
  "EmployeePersonGenderCode": "M",
  "EmployeePersonGenderName": "Male"
}
```

#### children

TODO

#### foreignKey

TODO
