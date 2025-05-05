# Experimentation JSON

In the `experimentationJson`, we have three important variables:

1. **chartwiseReqBody**
2. **chartSettingTemplate**
3. **commonFilter**

## Structure of `chartSettingTemplate`

```typescript
{
    "col": {
        "w": number, // width of the layout
        "h": number, // height of the layout
        "x": number, // start position on x axis of the layout
        "y": number, // start position on y axis of the layout
        "i": string  // unique id for the layout
    },
    "pannel": {
        "config": {
            "heading": string[], // query string
            "customHeading": string, // custom heading for chart
            "groupByDetails": [ 
                {
                    "label": string, // stores the column name 
                    "dataType": string, // stores the data type
                    "uniqueValues": string[], // store the unique values for the selected column
                    "selectedValues": string[], // stores the selected value
                    "totalRecordCount": number,
                    "filteredRecordCount": number,
                    "limit": number,
                    "searchString": string,
                    "isLoading": boolean
                }
            ],
            "interaction": string, // stores the chart name of the interacted chart
            "interactionChartID": string, // stores the chart id of the interacted chart
            "interactionFilterFiled": string, // stores the selected field on the interacted chart
            "interactionFilterValue": string, // stores the selected value on the interacted chart
            "containsInsight": boolean, 
            "multiInteractionField": [ // stores the selected field and selected value on the interacted chart
                {
                    "field": string,
                    "selectedValue": string,
                    "dataType": string,
                    "dateFormat": string
                }
            ],
            "integrateCondition": {
                "filter": boolean, // while interaction the parent chart filter need to affect current chart
                "byCondition": boolean, // while interaction the parent chart by condition need to affect current chart
                "allData": boolean // while interaction the values in parent is add as condition for current chart
            }
        },
        "chart": string, // id from chart details variable
        "chartID": string, // layout id like 'chart_i'
        "AIChart": boolean // flag for ai chart or user created chart
    }
}

```

## Structure of `chartwiseReqBody`

```typescript
{
    // list of item has current chart as parent and isInteractAll as true 
    "isInteractAllChildList": string[], 
    // current chart id
    "chartId": string,
    // when interaction the child need to clear for that child list send over here
    "childChartList": string[], 
    // across fields in qpad
    "groupBYParameter": GroupByParameterType[],
    // view fields in qpad
    "aggregateParameter": ChartYAxisType[],
    // says which chart is it 
    "chartType": string,
    // says whether the query is valid 
    "isValid": boolean,
    // by fields in qpad
    "byCondition": byConditionType[],
    // contains all/f100/ l100/ range and if any internal filter condition 
    "filter": FilterType,
    // contains the common filter condition
    "commonFilter": commonConditionFieldListType[],
    // contains the group by params need to show as date/month/quater/ year and all/date range/ 1 current week/ 2 current week/ 3current week  
    "dateRangeFilter": DateFilterType,
    // contains the latitude and longitude fields
    "coordinate": coordinateType,
    // containd one column name/ order_type / datatype
    "sortDetails": chartSortDetailsType[],
    // contains the aops fields
    "aopsDetails": aopsDetailsType[],
    // contains the selected fields from view fields in qpad
    "selectedViews": string[],
    // aops > display field > show list of column details
    "fieldList": displayFieldAopsType[],
    // gauge chart > properties > target value configuration > **field**/ constant > select field
    "targetFieldName": string, 
    // used inside filter whether current chart is inclued in common filter or not
    "isCommonFilterApplied": boolean, 
    // bubble chart > properties > show missing values
    "showNull": boolean, 
    // grouped reference and trend view > trend line settings in chart menu
    "trendDetails": TrendDetailsType,
    // show badge when sort is applied
    "sortIndicator": boolean, 
    // properties in charts menu
    "properties": chartPropsType,
    // says that common properties applied in current chart
    "isCommonPropertiesApplied": boolean, 
    // says that chart/ table need to show in layout
    "toggledView": string | null, 
    "tableProperties": tablePropertiesType[],
    "tableColumnSize": any,
    "setTableProperties": boolean,
    "quadrantDetails": any, 
    // during interaction get all parent contition
    "parentConditions": GetParentFilterDetailsReturnType,
    "tablePagination": tablePagi,
    // during interaction get all parent aops details
    "parentAOpsDetails": aopsDetailsType[], 
    // tells current chart is interacted with which chart
    "interactionChartId": string, 
    // tells current chart is interacted in all data mode
    "isInteractAllData": boolean, 
    // child chart list which chart has current chart as parent
    "chartList": ChartWiseReqBodyType[],
    // says the selected field / selected value / multiInteractField and child chart list which charts has current chart as parent
    "interactWith": interactionDataType, 
    // says that in parent chart any value is selected or not
    "isHighlight": boolean,
    // industrial standard in chart menu > helps to add line over trend
    "customTrendData": CustomTrendDataType 
}
 ```
 
 ### Parameters to be Explained

1. **groupBYParameter**  
    Contains the column which needs to be grouped in the query.  
    Maximum of 3 columns can be added.
   ```typescript
   {
        "columnName": "string",
        "isGroupByIsDateType": "boolean",
        "aliasName": "string",
        "dataType": "string"
    }
   ```

2. **aggregateParameter**  
   Contains the columns on which aggregate operations like min, max, sum, count, and avg need to be performed.  
   Any number of columns with different operation types can be added.
   ```typescript
    {
        "label": "string",
        "operationType": "string",
        "dataType": "string",
        "aliasName": "string"
    }
    ```

3. **byCondition**  
   Contains the conditions that need to be added (only in).
   ```typescript
    {
        field: string;
        dataType: string;
        selectedValues: string[];
    }
    ```

4. **filter**  
   Options include first 100, last 100, all, or a specific range.  
   Contains conditions that need to be added (e.g., =, !=, <, >, <=, >=).
   ```typescript
   {
        filterType: string;
        range?: {
            from: string;
            to: string;
        }
        filterColumn?: {
            field: string;
            operator: string;
            value: string | string[] | any;
            dataType: string;
            toValue: string | string[] | any;
            }[];
    }
   ```

5. **dateRangeFilter**  
    Group by date, month, quarter, or year.  
   Options include last, last two, or last three days/months/quarters/years, or based on a specific date range.
    ```typescript
    {
        category: string;
        selectDateOption: string;
        fromDate: string | null | undefined;
        toDate: string | null | undefined;
    }
    ```

6. **coordinate**  
    Contains latitude and longitude.
   ```typescript
   {
        latitude: string;
        longitude: string;
    }
   ```

7. **sortDetails**  
   Contains one column and the order type to sort in the query.
   ```typescript
   {
        columnName: string;
        dataType: string;
        sortType: string;
    }
   ```

8. **aopsDetails**  
   Used to perform arithmetic operations like +, -, *, /, and %.
   ```typescript
       {
        id: string;
        customFieldName: string;
        leftFieldType: string;
        leftFieldName: string;
        leftConstantValue: string;
        operation: string;
        rightFieldType: string;
        rightFieldName: string;
        rightConstantValue: string;
    }
   ```

9. **selectedViews**  
   Contains the views that need to be shown to the user.
   ```typescript
    string[]
   ```

10. **trendDetails**  
    Used to change the trend based on some arithmetic operations of views.
    ```typescript
     {
        properties: {
            id: string;
            customFieldName: string;
            customFieldNameValid: boolean;
            customFieldNameNotAmbiguous: boolean;
            leftFieldType: string;
            leftFieldName: string;
            leftFieldNameValid: boolean;
            leftConstantValue: string;
            leftConstantValueValid: boolean;
            operation: string;
            operationValid: boolean;
            rightFieldType: string;
            rightFieldName: string;
            rightFieldNameValid: boolean;
            rightConstantValue: string;
            rightConstantValueValid: boolean;
            isArithmeticOperatorEdited?: boolean;
        }[];
        groupingCategory: string;
        avgCalType: string;
        groupingCategoryValid: boolean;
        trendLineField?: string;
        trendLineFieldDatatype?: string;
    }
    ```

11. **customTrendData**  
    Allows adding some standard values over the trend.
    ```typescript
    {
        customFieldName: string,
        type: "INDIVIDUAL" | "COMMON";
        commonValue: string;
        isValid: boolean;
        trendData: {
            key: string;
            value: string;
        }[];
        dateCategory: string
    }
    ```

## Structure of `commonFilter`
contains the condition which apply for all selected charts (data and filter)
```typescript
{
    "chartType": string,
    "selectedChartList": string[],
    "fieldList": [
        {
            "field": string,
            "operator": string,
            "value": string | string[],
            "dataType": string,
            "toValue": string,
            "dateBasedOn": string,
            "totalRecordCount": number,
            "limit": number
        }
    ],
    "showTop": boolean,
    "isApplicableForUpcomingChart": boolean
}

