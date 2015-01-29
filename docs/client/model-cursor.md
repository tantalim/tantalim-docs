# ModelCursor
Part of `tantalim.common` the `ModelCursor` is created with a Model and a data set. It has two main jobs:

* Remember which records have been inserted, updated, and deleted
* Track which row is currently selected

Keeping track of the structure of the data model and navigating up, down and sideways can get complex. The ModelCursor
takes care of all of that complexity.

## Member Variables and Methods

### root

Every model has a top level array of records (instances).

### current

`current` is an object with two properties: `sets` and `instances`. This is a convenience object that helps AngularJS
know what record is the current record to display. It's similar in concept to a
[database cursor](http://en.wikipedia.org/wiki/Cursor_%28databases%29).

#### current.instances

An `instance` is defined as a single row and its child sets.
`current.instances` is an object map of viewName -> current instance. Usage:

```javascript
// returns the record that is currently being pointed to within the "Foo" view
return ModelCursor.current.instances["Foo"]
```

See [SmartNodeInstance](#smartnodeinstance)

#### current.sets

A `set` is defined as an array of SmartNodeInstances.
`current.sets` is an object map of viewName -> current set

See [SmartNodeSet](#smartnodeset)

#### modelMap

Object containing a map of "modelName" to the model definition along with the model's parent name as well.

## SmartNodeInstance

`id`: Unique row identifier

`data`: The map of columns and values for this instance

`nodeSet`: reference to the parent SmartNodeSet that contains this instance

`childModels`: map of SmartNodeInstances representing the children of this node

`state`: NO_CHANGE, DELETED, INSERTED, or UPDATED

## SmartNodeSet

`model.modelName`: Name of the model

`model.parentInstance`: Reference to the parent instance if any

`model.orderBy`: String - name of column to sort by or function - function to apply to row for sorting

`model.childModels`: Array of strings representing the name of each child model

`parent.instance`: The parent SmartNodeInstance of this SmartNodeSet, null if this instance is root

`parent.model`:

`currentIndex`:

`rows`: Array of SmartNodeInstances

`deleted`: Array of SmartNodeInstances that have been marked to delete
