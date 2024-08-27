# **Walmart E-commerce Sales Analysis Around Holidays**

## **Project Overview**
Walmart, the largest retail store in the United States, has seen significant growth in its e-commerce business, with sales reaching $80 billion by the end of 2022. Public holidays such as the Super Bowl, Labour Day, Thanksgiving, and Christmas are major contributors to this sales volume.

This project focuses on analyzing supply and demand around these holidays by building a data pipeline that processes and analyzes grocery sales data along with complementary data like weather, consumer price index (CPI), unemployment rates, and promotional markdowns.

## **Data Sources**
- **`grocery_sales` table (PostgreSQL)**: Contains data on weekly grocery sales at different Walmart stores.
  - **Columns**:
    - `index`: Unique ID of the row.
    - `Store_ID`: Store number.
    - `Date`: The week of sales.
    - `Weekly_Sales`: Sales for the given store.
  
- **`extra_data.parquet` file**: Contains additional data that complements the grocery sales data.
  - **Columns**:
    - `IsHoliday`: Indicates if the week contains a public holiday (1 if yes, 0 if no).
    - `Temperature`: Temperature on the day of sale.
    - `Fuel_Price`: Cost of fuel in the region.
    - `CPI`: Prevailing consumer price index.
    - `Unemployment`: Prevailing unemployment rate.
    - `MarkDown1`, `MarkDown2`, `MarkDown3`, `MarkDown4`: Number of promotional markdowns.
    - `Dept`: Department number in each store.
    - `Size`: Size of the store.
    - `Type`: Type of the store (based on the `Size` column).

## **Project Workflow**

### 1. **Data Extraction**
   - **Extract** data from the provided `grocery_sales` table and the `extra_data.parquet` file.
   - **Merge** these datasets on the `index` column to create a unified DataFrame.

### 2. **Data Transformation**
   - **Handle Missing Values**: Fill missing values in `CPI`, `Weekly_Sales`, and `Unemployment` columns with their respective means.
   - **Date Conversion**: Convert the `Date` column to datetime format and extract the month.
   - **Filtering**: Retain only rows where `Weekly_Sales` is greater than 10,000.
   - **Drop Columns**: Remove unnecessary columns like `index`, `Temperature`, `Fuel_Price`, `MarkDown1-4`, `Type`, `Size`, and `Date`.
   - **Store Cleaned Data**: Save the transformed data in a variable called `clean_data`.

### 3. **Data Aggregation**
   - **Calculate Monthly Sales**: Group the data by `Month` and calculate the average `Weekly_Sales`.
   - **Store Aggregated Data**: Save the results in a variable called `agg_data`.

### 4. **Data Loading**
   - **Save Cleaned Data**: Export `clean_data` to `clean_data.csv`.
   - **Save Aggregated Data**: Export `agg_data` to `agg_data.csv`.

### 5. **Validation**
   - **Validate Files**: Check if `clean_data.csv` and `agg_data.csv` have been created successfully.

## **Files and Directories**
- **`grocery_sales`**: SQL table containing weekly sales data.
- **`extra_data.parquet`**: Parquet file with complementary data.
- **`clean_data.csv`**: CSV file containing the cleaned and transformed data.
- **`agg_data.csv`**: CSV file containing the aggregated monthly sales data.

## **Tools & Libraries**
- **Pandas**: For data manipulation and analysis.
- **NumPy**: For numerical computations.
- **Logging**: For tracking the workflow execution.
- **OS**: For file validation and management.

## **How to Run the Project**
1. **Ensure all dependencies are installed**:
   ```bash
   pip install pandas numpy
