
# City of Chicago Yearly Budget Analysis - Pulling Data from API

Data is taken from the City of Chicago Data Portal website:

https://data.cityofchicago.org/

Specifically the 2011 through 2017 "Budget Ordinance - Positions and Salaries" APIs found in the Administration & Finance category


```python
#Dependencies
import pandas as pd
from sodapy import Socrata
from config import apikey
from pprint import pprint
```


```python
# Base url
url = "data.cityofchicago.org"

# authenticated client (needed for non-public datasets):
client = Socrata(url, apikey)

# Budget ordinance codes for 2011-2017
budget_eps = ["sgie-nk8s", "c5pd-qhn7", "vjc3-qwxu", "c3a6-cgvg", "2mkx-pejj", "d823-3fqq", "ghci-5ryk"]
```


```python
# set the first year of data to be pulled from the API
y = 2011

# Create an empty list to append the year for each row of data being pulled
year = []

# Create an empty data frame to append the yearly budget data to
overall_budget_df = pd.DataFrame()

# Loop through the yearly budget codes to pull relevant data from the API
for item in budget_eps:
    
    # Get results for a specific year and append to a data frame
    results = client.get(item, limit=10000)
    results_df = pd.DataFrame.from_records(results)
    
    # Column names are different for the 2011 data. Use this loop to make consistent with data from 2012-2017
    if y == 2011:
        results_df.rename(columns={'department_code': 'department_number', 'department_name': 'department_description',#\
                                  'division_name': 'division_description', 'fund_name': 'fund_description',\
                                  'section_name': 'section_description', 'subsection_code': 'sub_section_code',\
                                  'subsection_name': 'sub_section_description', 'total_budgeted_units': 'total_budgeted_unit'}, \
                          inplace=True)
    
    # append budget data to the empty dataframe above
    overall_budget_df = pd.concat([overall_budget_df,results_df])
    
    for x in range(0,len(results)):
        year.append(y)
    
    # Change to the next year in the budget list
    y = y + 1
```


```python
# Add the year column to the overall dataframe
overall_budget_df['year'] = year

# Print a sample of the dataframe
overall_budget_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>bargaining_unit</th>
      <th>budgeted_pay_rate</th>
      <th>budgeted_unit</th>
      <th>department</th>
      <th>department_code</th>
      <th>department_description</th>
      <th>department_number</th>
      <th>division_code</th>
      <th>division_description</th>
      <th>fund_code</th>
      <th>...</th>
      <th>schedule_grade</th>
      <th>section_code</th>
      <th>section_description</th>
      <th>sub_section_code</th>
      <th>sub_section_description</th>
      <th>title_code</th>
      <th>title_description</th>
      <th>total_budgeted_amount</th>
      <th>total_budgeted_unit</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>2485</td>
      <td>Annual</td>
      <td>CITY CLERK</td>
      <td>NaN</td>
      <td>CITY CLERK</td>
      <td>25</td>
      <td>2005</td>
      <td>City Clerk</td>
      <td>300</td>
      <td>...</td>
      <td>NaN</td>
      <td>3030</td>
      <td>Vehicle License Data Services</td>
      <td>0</td>
      <td>NaN</td>
      <td>15</td>
      <td>Schedule Salary Adjustments</td>
      <td>2485</td>
      <td>0</td>
      <td>2011</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>2389</td>
      <td>Annual</td>
      <td>DEPT OF FIN</td>
      <td>NaN</td>
      <td>DEPARTMENT OF FINANCE</td>
      <td>27</td>
      <td>2005</td>
      <td>City Comptroller</td>
      <td>610</td>
      <td>...</td>
      <td>NaN</td>
      <td>3030</td>
      <td>Auditing</td>
      <td>0</td>
      <td>NaN</td>
      <td>15</td>
      <td>Schedule Salary Adjustments</td>
      <td>2389</td>
      <td>0</td>
      <td>2011</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>73932</td>
      <td>Annual</td>
      <td>DEPT OF FIN</td>
      <td>NaN</td>
      <td>DEPARTMENT OF FINANCE</td>
      <td>27</td>
      <td>2005</td>
      <td>City Comptroller</td>
      <td>610</td>
      <td>...</td>
      <td>NaN</td>
      <td>3030</td>
      <td>Auditing</td>
      <td>0</td>
      <td>NaN</td>
      <td>102</td>
      <td>Accountant II</td>
      <td>73932</td>
      <td>1</td>
      <td>2011</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>76536</td>
      <td>Annual</td>
      <td>TREAS</td>
      <td>NaN</td>
      <td>CITY TREASURER</td>
      <td>28</td>
      <td>2005</td>
      <td>City Treasurer</td>
      <td>100</td>
      <td>...</td>
      <td>NaN</td>
      <td>3015</td>
      <td>Financial Reporting</td>
      <td>0</td>
      <td>NaN</td>
      <td>104</td>
      <td>Accountant IV</td>
      <td>76536</td>
      <td>1</td>
      <td>2011</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>88140</td>
      <td>Annual</td>
      <td>TREAS</td>
      <td>NaN</td>
      <td>CITY TREASURER</td>
      <td>28</td>
      <td>2005</td>
      <td>City Treasurer</td>
      <td>100</td>
      <td>...</td>
      <td>NaN</td>
      <td>3015</td>
      <td>Financial Reporting</td>
      <td>0</td>
      <td>NaN</td>
      <td>104</td>
      <td>Accountant IV</td>
      <td>88140</td>
      <td>1</td>
      <td>2011</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 26 columns</p>
</div>




```python
# Make a clean dataframe with desired columns
budget_by_year = overall_budget_df[['year', 'fund_type', 'fund_code', 'fund_description', 'department_number', 'department_description', \
                                   'organization_code', 'division_code', 'division_description', 'section_code', 'section_description', \
                                   'title_code', 'title_description', 'budgeted_unit', 'total_budgeted_unit', 'budgeted_pay_rate', \
                                   'total_budgeted_amount']]
```


```python
# print head of dataframe
budget_by_year.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>fund_type</th>
      <th>fund_code</th>
      <th>fund_description</th>
      <th>department_number</th>
      <th>department_description</th>
      <th>organization_code</th>
      <th>division_code</th>
      <th>division_description</th>
      <th>section_code</th>
      <th>section_description</th>
      <th>title_code</th>
      <th>title_description</th>
      <th>budgeted_unit</th>
      <th>total_budgeted_unit</th>
      <th>budgeted_pay_rate</th>
      <th>total_budgeted_amount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2011</td>
      <td>Local</td>
      <td>300</td>
      <td>VEHICLE FUND</td>
      <td>25</td>
      <td>CITY CLERK</td>
      <td>1005</td>
      <td>2005</td>
      <td>City Clerk</td>
      <td>3030</td>
      <td>Vehicle License Data Services</td>
      <td>15</td>
      <td>Schedule Salary Adjustments</td>
      <td>Annual</td>
      <td>0</td>
      <td>2485</td>
      <td>2485</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011</td>
      <td>Local</td>
      <td>610</td>
      <td>MIDWAY AIRPORT FUND</td>
      <td>27</td>
      <td>DEPARTMENT OF FINANCE</td>
      <td>1005</td>
      <td>2005</td>
      <td>City Comptroller</td>
      <td>3030</td>
      <td>Auditing</td>
      <td>15</td>
      <td>Schedule Salary Adjustments</td>
      <td>Annual</td>
      <td>0</td>
      <td>2389</td>
      <td>2389</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2011</td>
      <td>Local</td>
      <td>610</td>
      <td>MIDWAY AIRPORT FUND</td>
      <td>27</td>
      <td>DEPARTMENT OF FINANCE</td>
      <td>1005</td>
      <td>2005</td>
      <td>City Comptroller</td>
      <td>3030</td>
      <td>Auditing</td>
      <td>102</td>
      <td>Accountant II</td>
      <td>Annual</td>
      <td>1</td>
      <td>73932</td>
      <td>73932</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2011</td>
      <td>Local</td>
      <td>100</td>
      <td>CORPORATE FUND</td>
      <td>28</td>
      <td>CITY TREASURER</td>
      <td>1005</td>
      <td>2005</td>
      <td>City Treasurer</td>
      <td>3015</td>
      <td>Financial Reporting</td>
      <td>104</td>
      <td>Accountant IV</td>
      <td>Annual</td>
      <td>1</td>
      <td>76536</td>
      <td>76536</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2011</td>
      <td>Local</td>
      <td>100</td>
      <td>CORPORATE FUND</td>
      <td>28</td>
      <td>CITY TREASURER</td>
      <td>1005</td>
      <td>2005</td>
      <td>City Treasurer</td>
      <td>3015</td>
      <td>Financial Reporting</td>
      <td>104</td>
      <td>Accountant IV</td>
      <td>Annual</td>
      <td>1</td>
      <td>88140</td>
      <td>88140</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Convert budget information from string to float
budget_by_year["total_budgeted_amount"] = budget_by_year["total_budgeted_amount"].astype(float)
```

    C:\Users\hbs49\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      from ipykernel import kernelapp as app
    


```python
# check to ensure the budget information is now float
budget_by_year["total_budgeted_amount"].max()
```




    189413136.0




```python
# Convert pay rate information from string to float
budget_by_year["budgeted_pay_rate"] = budget_by_year["budgeted_pay_rate"].astype(str)
budget_by_year["budgeted_pay_rate"] = budget_by_year["budgeted_pay_rate"].astype(float)
```

    C:\Users\hbs49\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      from ipykernel import kernelapp as app
    C:\Users\hbs49\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      app.launch_new_instance()
    


```python
# check to ensure the pay rate information is now float
budget_by_year["budgeted_pay_rate"].max()
```




    51455255.0




```python
# write the data from to a csv
budget_by_year.to_csv("budget_by_year.csv", index=False)
```
