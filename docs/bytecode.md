# Model Bytecode

modeCompiler.js takes model src (json source) along with any needed table src (json source) and compiles it into a more
computer friendly format.

You need to be familiar with this content ONLY if you're programming on the Tantalim source code. Otherwise refer to [Model](models)

## Model Definition

```json
{
  "name": "BuildTable",
  "moduleName": "tantalim-ide",
  "basisTable": {
    "name": "Table",
    "dbName": "db_table"
  },
  "instanceID": "TableID",
  "limit": 10,
  "orderBy": [ARRAY_OF_ORDER_CLAUSES],
  "fields": [ARRAY_OF_FIELD_DEFINITIONS],
  "steps": [ARRAY_OF_STEPS],
  "children": [ARRAY_OF_MODEL_DEFINITONS]
}
```

Below are descriptions of properties found only in the model. For all other descriptions, refer to [Model](models)
documentation.

#### name

The unique programmatic name for this model. Added during compilation automatically from the name of the artifact.

#### moduleName

The module this definition came from.

TODO: figure out if and when we'll need to consider the "package" or application module this model is in. Hopefully, we
can do it like most programming languages, ie. assume the modelName refers to a model in this module or application or
list the module along with the modelName.

#### basisTable

Transformed from a `string` to an `object` during compilation. See [basisTable](models#basistable).

#### instanceID

Optional field name of this instance's (row's) unique identifier. Previously called `primaryKey`. Derived from the
basis table's primary key during compilation.

## Steps

Steps go through a lot of transformation during the compilation phase. Source code (see [Model Step](models/#steps))
is converted to this:

```json
    {
      "name": "FromTableToModule",
      "required": false, // from step.required or step.join.required or false (default)
      "join": {
        "name": "ToModule",
        "table": {
          "name": "Module",
          "dbName": "app_module"
        },
        "columns": [
          {
            "from": {
              "name": "ModuleID",
              "dbName": "moduleID"
            },
            "to": {
              "name": "ModuleID",
              "dbName": "moduleID"
            }
          }
        ]
      },
      "stepCount": 1
    }
    {
      "name": "FromTableToModule",
      "joinToTableSql": "app_module",
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
  },
  "dataType": "String",
  "fieldDefault": {
    "type": "field",
    "value": "TableName",
    "updateable": false
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
