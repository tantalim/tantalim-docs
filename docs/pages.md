# Page Layer

Rich functionality, custom scripts, and business logic

## Page Definition

```json
{
    "id": "SamplePage",
    "title": "Build Table",
    "viewMode": "single",
    "modelName": "TableColumns",
    "parentModel": "BuildTable",
    "depth": 1,
    "multiPage": true,
    "breadcrumb": [ARRAY_OF_BREADCRUMBS] (maybe should be plural?)
        {
            "pageID": "BuildTable",
            "modelName": "ManageTables",
            "field": "TableName"
        }
    ],
    "orderBy": "TableColumnDisplayOrder",
    "splitFields": [ARRAY_OF_FIELDS],
    "quickView": [ARRAY_OF_FIELDS],
    "listFields": [ARRAY_OF_FIELDS],
    "formFields": [ARRAY_OF_FIELDS],
    "buttons": [ARRAY_OF_BUTTONS],
    "children": [ARRAY_OF_PAGES],
}
```
See also: [Field Definitions](#field-definition)

### id

Required String. Unique identifier for page. This is usually a GUID but can be an alpha-numeric string.

### title

Required String. User friendly page title that will be displayed on menus and at the top of each single page app.

### viewMode

Optional Enumeration. The default starting display mode. Must be one of the following:
* single
* multiple

### modelName

Required String. The unique identifier of the model layer matching this page.

### parentModel

Optional String. The unique identifier of the model layer matching this page's parent. TODO: explain why this is needed and can't be inferred.

### depth

Optional Integer. Positive integer that describes the number of levels below the parent.

### multiPage

Optional Boolean. Equals Yes, if the single page app has multiple pages (such as parent-child).

## Field Definition

### Json Sample
```json
{
    "fieldName": "SampleField",
    "fieldLabel": "Sample Field",
    "fieldType": "checkbox",
    "select": {
        "model": "ListTables",
        "display": "TableName",
        "copy": [
            {
                "from": "TableTableID",
                "to": "TableJoinToTableID"
            }
        ],
        "where": [
            {
                "TBD": "TODO"
            }
        ]
    },
    "disabled": true,
    "fieldHelp": "This is a sample help text."
}
```

### fieldName

Required String. Unique identifier for field. This is usually a programmer friendly alpha-numeric string without special characters and spaces.

### fieldLabel

Required String. User friendly label for the field that will be visible in the column header and prompt.

### fieldType

Optional Enumeration. The type of field display. Must be one of the following:

* string (default)
* number
* checkbox
* select (aka smartselect)
* radio
* textarea
* date

### disabled

Optional Boolean. Enabled by default, disabled=false.

### fieldHelp

Optional String. Longer help text in HTML for end users.<br> This feature is coming soon.

### select

Optional Object. Required if fieldType = select. Provides detailed definition for Smart Select boxes.

#### select.model

Required String. Name of the unique identifier for the Model to query for this Select.
TODO: support models with values already listed.

