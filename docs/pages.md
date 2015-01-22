# Page Layer

Rich functionality, custom scripts, and business logic

Page Definition

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

<table class="table table-bordered">
    <thead>
    <tr>
        <th>Field Name</th>
        <th>Required</th>
        <th>Data Type</th>
        <th>Description</th>
    </tr>
    </thead>
    <tbody class="table-hover">
        <tr>
            <td>id</td>
            <td>Yes</td>
            <td>String</td>
            <td>Unique identifier for page. This is usually a GUID but can be an alpha-numeric string.</td>
        </tr>
        <tr>
            <td>title</td>
            <td>Yes</td>
            <td>String</td>
            <td>User friendly page title that will be displayed on menus and at the top of each single page app.</td>
        </tr>
        <tr>
            <td>viewMode</td>
            <td>No</td>
            <td>Enumeration</td>
            <td>The default starting display mode. Must be one of the following:
                <ul>
                    <li>single</li>
                    <li>multiple</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>modelName</td>
            <td>Yes</td>
            <td>String</td>
            <td>The unique identifier of the model layer matching this page.</td>
        </tr>
        <tr>
            <td>parentModel</td>
            <td>No</td>
            <td>String</td>
            <td>The unique identifier of the model layer matching this page's parent. TODO: explain why this is needed and can't be inferred.</td>
        </tr>
        <tr>
            <td>depth</td>
            <td>No</td>
            <td>Integer</td>
            <td>Positive integer that describes the number of levels below the parent.</td>
        </tr>
        <tr>
            <td>multiPage</td>
            <td>No</td>
            <td>Boolean</td>
            <td>Yes, if the single page app has multiple pages (such as parent-child).</td>
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
        </tr>
    </tbody>
</table>

## Field Definition

```json
{
    "fieldName": "SampleField",
    "fieldLabel": "Sample Field",
    "fieldType": "checkbox",
    "select": {
        "model": "ListTables",
        "display": "TableName",
        "copy": [ARRAY_OF_COPY_DIRECTIONS],
        {
        "from": "TableTableID",
        "to": "TableJoinToTableID"
        }
        ],
        "where": [ARRAY_OF_WHERE_CLAUSES]
    },
    "disabled": true,
    "fieldHelp": "This is a sample help text."
}
```

<table class="table table-bordered">
    <thead>
    <tr>
        <th>Field Name</th>
        <th>Data Type</th>
        <th>Description</th>
    </tr>
    </thead>
    <tbody class="table-hover">
    <tr>
        <td>fieldName</td>
        <td>String</td>
        <td>Unique identifier for field. This is usually a programmer friendly alpha-numeric string without special characters and spaces.</td>
    </tr>
    <tr>
        <td>fieldLabel</td>
        <td>String</td>
        <td>User friendly label for the field that will be visible in the column header and prompt.</td>
    </tr>
    <tr>
        <td>fieldType</td>
        <td>Enumeration</td>
        <td>The type of field display. Must be one of the following:
        <ul>
            <li>string (default)</li>
            <li>number</li>
            <li>checkbox</li>
            <li>select (aka smartselect)</li>
            <li>radio</li>
            <li>textarea</li>
            <li>date</li>
        </ul></td>
    </tr>
    <tr>
        <td>disabled</td>
        <td>boolean</td>
        <td>Enabled by default, disabled=false.</td>
    </tr>
    <tr>
        <td>fieldHelp</td>
        <td>String</td>
        <td>Longer help text in HTML for end users.<br> This feature is coming soon.</td>
    </tr>
    </tbody>
</table>
