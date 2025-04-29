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
    "isInteractAllChildList": string[], 
    "chartId": string,
    "childChartList": string[], 
    "groupBYParameter": GroupByParameterType[],
    "aggregateParameter": ChartYAxisType[],
    "chartType": string,
    "isValid": boolean,
    "byCondition": byConditionType[],
    "filter": FilterType,
    "commonFilter": commonConditionFieldListType[], 
    "dateRangeFilter": DateFilterType,
    "coordinate": coordinateType,
    "sortDetails": chartSortDetailsType[],
    "aopsDetails": aopsDetailsType[],
    "selectedViews": string[],
    "fieldList": displayFieldAopsType[],
    "targetFieldName": string, 
    "isCommonFilterApplied": boolean, 
    "showNull": boolean, 
    "trendDetails": TrendDetailsType,
    "sortIndicator": boolean, 
    "properties": chartPropsType,
    "isCommonPropertiesApplied": boolean, 
    "toggledView": string | null, 
    "tableProperties": tablePropertiesType[],
    "tableColumnSize": any,
    "setTableProperties": boolean,
    "quadrantDetails": any, 
    "parentConditions": GetParentFilterDetailsReturnType,
    "tablePagination": tablePagi,
    "parentAOpsDetails": aopsDetailsType[], 
    "interactionChartId": string, 
    "isInteractAllData": boolean, 
    "chartList": ChartWiseReqBodyType[],
    "interactWith": interactionDataType, 
    "isHighlight": boolean,
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

