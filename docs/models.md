# Models

```json
{
  "basisTable": "TableName",
  "limit": 10,
  "allowInsert": true,
  "allowUpdate": true,
  "allowDelete": true,
  "orderBy": [ARRAY_OF_ORDER_CLAUSES],
  "parentLink": {
    "parentField": "TableID",
    "childField": "ParentID"
  },
  "children": [ARRAY_OF_MODEL_DEFINITIONS],
  "fields": [ARRAY_OF_FIELD_DEFINITIONS],
  "steps": [ARRAY_OF_STEPS]
}
```

#### name

This is implied by the name of the file such as `Person.json`. Don't include this in the definition.
This name is the programmatic name and it's used by things such as [Page.model](pages#model).

#### basisTable

Tantalim data architecture is based on a simple concept that joins always travel from many-to-one or one-to-one unless
incorporating a child set of records (one-to-many). The basis table (or tables in the case of a multi-view model) keeps
all the data in the view together. All other fields should be reachable from a M:1 or 1:1 join.

#### limit

The default limit of records that can be retrieved without paging. In general, models with a lot of fields should use a
smaller limit. "Thin" models with no children and just a few fields can have a very high limit.

#### allowInsert

Optional Boolean true or false. Defaults to `true`.

#### allowUpdate

Optional Boolean true or false. Defaults to `true`.

#### allowDelete

Optional Boolean true or false. Defaults to `true`.

#### orderBy

The default order by clause if one is not supplied at runtime.

```json
{
  "fieldName": "TableName",
  "direction": "ASC"
}
```
Above is a typical order by clause.

* `fieldName` is the programmatic field as listed in this model.
* `direction` is the sort order such as ASC (default) or DESC.

#### parentLink

Required only for child models. The `parentField` is a string that refers to the name of one field in the parent view.
The `childField` is a string that refers to the name of one field in the current (child) view. On insert (and update),
the childField will always default it's value from the parentField. This behavior is automatic and does not require a
column default.

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
  "basisColumn": "Name",
  "required": false,
  "updateable": true
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

#### required

Optional Boolean value if the column is required. Defaults to [Table.required](tables#required).

#### updateable

Optional Boolean value if the column can be changed. Defaults to [Table.updateable](tables#updateable).

