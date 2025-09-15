# 🔘 UI elements

The following subchapters of the tree describe the components that the application commonly uses.

Elements that are not listed in the tree can be created as standard JavaScript **input** elements. The functions below will help you create these elements.

If possible, prefer to use the entire plugin (for example, with a button and action).

## Application-side support

These subchapters describe individual functions and their parameters.

### appendField

Creates a new **INPUT** field with a label that marks the element when clicked.

| Parameter | Default | Description |
|---|---|---|
| target | required | Target parent element |
| id | required | ID of the new element. The localization system uses the element ID to automatically pair its keys on the UI |
| defaultV | '' | Default value of the element |
| type | FormFieldType.TEXT | Field type. FormFieldType contains values that can be used. Values: TEXT, CHECKBOX, FILE |

### appendFieldComboBox

Creates a new **select/combobox** field with a label that will be selected when clicked.

| Parameter | Default | Description |
|---|---|---|
| target | required | Target parent element |
| id | required | ID of the new element. The localization system uses the element ID to automatically pair its keys on the UI |

### appendComboBoxItems

Adds a list of items to an existing **select/combobox** field.

| Parameter | Default | Description |
|---|---|---|
| combobox | required | HTML combobox element |
| items | required | Array of item names. |
| defaultV | required | The value to be marked as default (preselected). It can be specified by the item text or index (the internal logic automatically numbers the items with an index in items). |
