# Tantalim SmartSelect

Creating dynamic select boxes can get complex very fast. Tantalim comes with a robust and full featured selection tool called SmartSelect.

## From the [server](server/)

```html
<ui-select ng-model="current.instances.{{../../modelName}}.data.{{fieldName}}"
           tnt-model="current.instances.{{../../modelName}}"
           tnt-copy="{{json this.select.copy}}"
           id="{{../../modelName}}-{{fieldName}}">
    <match placeholder="Select..." />
    <choices repeat="row in listSmartSelect.{{select.model}} track by row.id"
             refresh="runSmartSelect('{{this.select.model}}', '{{../../modelName}}', $select.search)"
             refresh-delay="0">
        <div ng-bind-html="row.data.{{select.display}} | highlight: $select.search"></div>
    </choices>
</ui-select>
```

## From the [client](client/)

```JavaScript
$scope.listSmartSelect = {};
$scope.runSmartSelect = function (sourceModel, modelName, queryValue) {
    PageService.queryModelData(sourceModel, queryValue).then(function (d) {
        $scope.listSmartSelect[sourceModel] = d.data;
    });
};
// this doesn't appear to be used anywhere??
$scope.chooseSmartSelect = function (modelName, copyFields, row) {
    ModelCursor.current.instances[modelName].selectOption(row, copyFields);
    ModelCursor.change(ModelCursor.current.instances[modelName]);
};
```

## Sequence Diagram

runSmartSelect
