# Tantalim SmartSelect

Creating dynamic select boxes can get complex very fast. Tantalim comes with a robust and full featured selection tool called SmartSelect.

## From the [FieldDefinition](pages/#select)

```json
{
    "fieldName": "TableModuleName",
    "fieldLabel": "Module",
    "fieldType": "select",
    "select": {
        "model": "ListModules",
        "targetID": "TableModuleID",
        "sourceValue": "ModuleModuleName",
        "otherMappings": [
            {
                "source": "ModuleModuleCode",
                "target": "TableModuleCode"
            }
        ],
        "where": []
    }
}
```
[Source](https://github.com/tantalim/app-ide/blob/master/app/tantalim/ide/pages/ListTables.json#L55)

## From the [server](server/)

```html
<ui-select
        item-model="{{select.model}}"
        item-value="{{select.sourceValue}}"
        instance-model="{{../../modelName}}"
        instance-key="{{select.targetID}}"
        instance-value="{{fieldName}}"
        other-mappings="{{json this.select.otherMappings}}"
        >
</ui-select>
```
[Source](https://github.com/tantalim/tantalim-server/blob/master/app/views/partials/html_view_single.html#L13)

