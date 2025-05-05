# Query String

The query string can be changed in two different ways:

### 1. **Using QPad**
- A filtered column list is shown under **view**, **across**, and **by** options.
- Once the required fields are selected, clicking **Apply** triggers the `generate` handler.
- This updates the `heading` variable in the `ChartSettingTemplate`.

### 2. **Using Query String Directly**
- Suggestions are shown in an autocomplete list from `autocompleteOption`.
- When the input changes (`onChange`), it updates the `heading` variable in the `ChartSettingTemplate`.

---

### Valid Query String Examples:

1. `view operation_type column_name_1`  
2. `view operation_type column_name_1 across column_name_2`  
3. `view operation_type column_name_1 across column_name_2 by column_name_3`

---

### Notes:

1. The `operation_type` must be one of the following: `sum`, `avg`, `min`, `max`, `count`, `distinct`.  
2. The `column_name` values must be present in the **filtered column list**.  
3. The **filtered column list** is created by selecting or unselecting columns in **Profile** and **Statics**.
