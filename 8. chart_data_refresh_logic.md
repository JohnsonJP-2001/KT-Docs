# Chart Data Refresh Logic

When a query is updated in the Query Pad or when filters, sorting, properties, or trend settings are applied, Tarvah evaluates the chart's interaction state to determine the appropriate data-fetching logic. There are three primary use cases:

## 1. Child Chart with Active Interaction (All Data)

**Condition:**
- The current chart is a child chart that is:
  - Interacted with another chart (parent), and
  - The "All Data" option is enabled in the Interaction Popper or a value is selected in the parent chart.

**Action:**
- Invoke the `getInterlinkChartDataNew` action with the appropriate request JSON.

## 2. Parent Chart with Active Children (All Data)

**Condition:**
- The current chart is a parent of one or more other charts, and those child charts have the "All Data" option enabled in their Interaction Popper.

**Action:**
- Invoke the `getInterlinkChartDataNew` action with the necessary request JSON.

## 3. Standard Chart (Non-Interacted or Inactive Interaction)

**Condition:**
- The current chart is not involved in any interaction, or
- It is a child chart, but no value is selected in the parent chart and the "All Data" option is not enabled.

**Action:**
- Invoke the `getChartData` action with the appropriate request JSON.
