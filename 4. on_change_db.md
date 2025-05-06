# Dataset Change Process in Tarvah

When changing the dataset in Tarvah, the following steps are taken to ensure that existing experiments and charts remain valid:

## Scenario
- **Current Experiment**: `experiment_1` created using `dataset_1`.
- **Columns in dataset_1**:
  - company
  - clientcode
  - consigneename
  - consignorname
  - shipmenttype
  - incoterms
  - shipmentno
  - origin
  - origincountry

- **Created Charts**:
  - **charts_1**: View count of `shipmenttype` from `clientcode`.
  - **charts_2**: View count of `clientcode` from `company`.

## Steps for Changing Dataset

### 1. Change Dataset
- User changes the dataset from `dataset_1` to `dataset_2`.

### 2. New Dataset Details
- **Columns in dataset_2**:
  - company
  - clientcode
  - consigneename
  - consignorname
  - shipmenttype
  - incoterms
  - origin
  - origincountry

### 3. Compare Columns
- Retrieve the column details from `dataset_2`.
- Compare the columns used in the query of each chart created in `experiment_1` with the columns in `dataset_2`.

### 4. Identify Missing Columns
- Identify any columns that are:
  - Present in `dataset_1` but missing in `dataset_2`.
  - Used in the chart queries (e.g., `shipmentno` in `charts_1`).

### 5. Missing Columns Notification
- If any columns used in the chart queries are missing in `dataset_2`, prompt the user with a confirmation message:
  - **Message**: "The following columns are missing in the new dataset: [list of missing columns used in charts]. Do you want to continue?"

### 6. User Response
- **If User Clicks "Continue"**:
  - Validate the chart queries against the new dataset.
  - Retrieve data for valid queries.
  - Update the charts with the new data.

- **If User Clicks "Cancel"**:
  - Abort the dataset change process and retain the current dataset.

## Conclusion
This process ensures that users are aware of any potential issues with their charts when changing datasets and allows them to make informed decisions on whether to proceed.
