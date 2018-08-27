
# City of Chicago Yearly Budget Analysis - Data Cleanup & Exploration

## Sources

Data is taken from the City of Chicago Data Portal website:

https://data.cityofchicago.org/

Specifically the 2011 through 2017 "Budget Ordinance - Positions and Salaries" APIs found in the Administration & Finance category

CAFR - Comprehensive Annual Financial Reports for the City of Chicago

## Read in the Data

- City of Chicago Budgets (by Department) from 2011 to 2017
- City of Chicago Financial Information from 2011 to 2016


```python
#Dependencies
import pandas as pd
```


```python
# Store filepath in a variable
budget_data = "budget_by_year.csv"
financial_data = "City.Chicago.Financials.csv"
```


```python
# Read our Data file with the pandas library
budget_by_year_df = pd.read_csv(budget_data, encoding="ISO-8859-1")
yearly_financials = pd.read_csv(financial_data, encoding="ISO-8859-1")
```

## Clean and Format the City Budget Data


```python
# Cleaning the department description to eliminate descrepancies in department descriptions between years
budget_by_year_df['department_description'].replace('BUS AFFAIRS AND CONSUMER PROT', \
                                                    'BUSINESS AFFAIRS AND CONSUMER PROTECTION', inplace=True)
budget_by_year_df['department_description'].replace('DOIT', \
                                                    'DEPARTMENT OF INNOVATION & TECHNOLOGY', inplace=True)
budget_by_year_df['department_description'].replace('FINANCE', \
                                                    'DEPARTMENT OF FINANCE', inplace=True)
budget_by_year_df['department_description'].replace('IPRA', \
                                                    'INDEPENDENT POLICE REVIEW AUTHORITY', inplace=True)
budget_by_year_df['department_description'].replace(['FLEET AND FACILITY MANAGEMENT', 'FLEET AND FACILITY MGMT'], \
                                                    'DEPARTMENT OF FLEET MANAGEMENT', inplace=True)
budget_by_year_df['department_description'].replace('OEMC', \
                                                    'OFFICE OF EMERGENCY MANAGEMENT & COMMUNICATIONS', inplace=True)
budget_by_year_df['department_description'].replace(['IG', 'OIG'], \
                                                    'INSPECTOR GENERAL', inplace=True)
budget_by_year_df['department_description'].replace('PLANNING AND DEVELOPMENT', \
                                                    'HOUSING AND ECONOMIC DEVELOPMT', inplace=True)
budget_by_year_df['department_description'].replace('ADMINISTRATIVE HEARINGS', \
                                                    'DEPT OF ADMINISTRATIVE HEARING', inplace=True)
budget_by_year_df['department_description'].replace('ANIMAL CARE AND CONTROL', \
                                                    'COMM ANIMAL CARE AND CONTROL', inplace=True)
budget_by_year_df['department_description'].replace('BACP', \
                                                    'BUSINESS AFFAIRS AND CONSUMER PROTECTION', inplace=True)
budget_by_year_df['department_description'].replace('CDOT', \
                                                    'CHICAGO DEPT OF TRANSPORTATION', inplace=True)
budget_by_year_df['department_description'].replace('DCASE', \
                                                    'CULTURAL AFFAIRS SPECIAL EVENT', inplace=True)
budget_by_year_df['department_description'].replace('DEPARTMENT OF BUILDINGS', \
                                                    'DEPT OF BUILDINGS', inplace=True)
budget_by_year_df['department_description'].replace('PROCUREMENT SERVICES', \
                                                    'DEPARTMENT OF PROCUREMENT SERV', inplace=True)
budget_by_year_df['department_description'].replace('STREETS AND SANITATION', \
                                                    'DEPT STREETS AND SANITATION', inplace=True)
budget_by_year_df['department_description'].replace('OBM', \
                                                    'OFFICE OF BUDGET & MANAGEMENT', inplace=True)
budget_by_year_df['department_description'].replace('WATER MANAGEMENT', \
                                                    'DEPT OF WATER MANAGEMENT', inplace=True)
budget_by_year_df['department_description'].replace('MOPD', \
                                                    'MAYORS OFFICE-DISABILITIES', inplace=True)
budget_by_year_df['department_description'].replace('CHICAGO FIRE DEPARTMENT', \
                                                    'FIRE DEPARTMENT', inplace=True)
budget_by_year_df['department_description'].replace('CHICAGO POLICE DEPARTMENT', \
                                                    'DEPARTMENT OF POLICE', inplace=True)
```

### Find the number of employees paid annualy 

- per year
- per department


```python
# Pull annual salaried employees into a dataframe
annual_df = budget_by_year_df.loc[budget_by_year_df["budgeted_unit"] == "Annual", :]
annual_df.head()
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
      <td>25.0</td>
      <td>CITY CLERK</td>
      <td>1005</td>
      <td>2005.0</td>
      <td>City Clerk</td>
      <td>3030.0</td>
      <td>Vehicle License Data Services</td>
      <td>15</td>
      <td>Schedule Salary Adjustments</td>
      <td>Annual</td>
      <td>0</td>
      <td>2485.0</td>
      <td>2485.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011</td>
      <td>Local</td>
      <td>610</td>
      <td>MIDWAY AIRPORT FUND</td>
      <td>27.0</td>
      <td>DEPARTMENT OF FINANCE</td>
      <td>1005</td>
      <td>2005.0</td>
      <td>City Comptroller</td>
      <td>3030.0</td>
      <td>Auditing</td>
      <td>15</td>
      <td>Schedule Salary Adjustments</td>
      <td>Annual</td>
      <td>0</td>
      <td>2389.0</td>
      <td>2389.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2011</td>
      <td>Local</td>
      <td>610</td>
      <td>MIDWAY AIRPORT FUND</td>
      <td>27.0</td>
      <td>DEPARTMENT OF FINANCE</td>
      <td>1005</td>
      <td>2005.0</td>
      <td>City Comptroller</td>
      <td>3030.0</td>
      <td>Auditing</td>
      <td>102</td>
      <td>Accountant II</td>
      <td>Annual</td>
      <td>1</td>
      <td>73932.0</td>
      <td>73932.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2011</td>
      <td>Local</td>
      <td>100</td>
      <td>CORPORATE FUND</td>
      <td>28.0</td>
      <td>CITY TREASURER</td>
      <td>1005</td>
      <td>2005.0</td>
      <td>City Treasurer</td>
      <td>3015.0</td>
      <td>Financial Reporting</td>
      <td>104</td>
      <td>Accountant IV</td>
      <td>Annual</td>
      <td>1</td>
      <td>76536.0</td>
      <td>76536.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2011</td>
      <td>Local</td>
      <td>100</td>
      <td>CORPORATE FUND</td>
      <td>28.0</td>
      <td>CITY TREASURER</td>
      <td>1005</td>
      <td>2005.0</td>
      <td>City Treasurer</td>
      <td>3015.0</td>
      <td>Financial Reporting</td>
      <td>104</td>
      <td>Accountant IV</td>
      <td>Annual</td>
      <td>1</td>
      <td>88140.0</td>
      <td>88140.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# List of years in the data set
years = [2011, 2012, 2013, 2014, 2015, 2016, 2017]

# Empty dataframe to append employee counts to
dep_count = pd.DataFrame()

# loop through the annual salaried employee datafrome by year
for year in years:
    
    # Create a dataframe for a specific year
    aby_df = annual_df.loc[annual_df["year"] == year, :]
    
    # Create a groupby object based on department
    aby_gp = aby_df.groupby("department_description")
    
    # Sum the number of annual salaried employees per department   
    aby_dep_count = aby_gp["total_budgeted_unit"].sum()
    
    # append to the employee count datafrome
    dep_count.loc[:, f"{year} Dept Annual Employees"] = aby_dep_count
```

### Find the number of employees paid monthly 

- per year
- per department


```python
# Pull monthly salaried employees into a dataframe
monthly_df = budget_by_year_df.loc[budget_by_year_df["budgeted_unit"] == "Monthly", :]
monthly_df.head()
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
      <th>427</th>
      <td>2011</td>
      <td>Local</td>
      <td>300</td>
      <td>VEHICLE FUND</td>
      <td>25.0</td>
      <td>CITY CLERK</td>
      <td>1005</td>
      <td>2005.0</td>
      <td>City Clerk</td>
      <td>3025.0</td>
      <td>Issuance of Vehicle Licenses</td>
      <td>429</td>
      <td>Clerk II</td>
      <td>Monthly</td>
      <td>24</td>
      <td>2298.0</td>
      <td>55152.0</td>
    </tr>
    <tr>
      <th>693</th>
      <td>2011</td>
      <td>Local</td>
      <td>100</td>
      <td>CORPORATE FUND</td>
      <td>29.0</td>
      <td>DEPARTMENT OF REVENUE</td>
      <td>1005</td>
      <td>2003.0</td>
      <td>Department of Revenue</td>
      <td>3154.0</td>
      <td>Payment Processing</td>
      <td>235</td>
      <td>Payment Services Representative</td>
      <td>Monthly</td>
      <td>12</td>
      <td>3036.0</td>
      <td>36432.0</td>
    </tr>
    <tr>
      <th>785</th>
      <td>2011</td>
      <td>Local</td>
      <td>100</td>
      <td>CORPORATE FUND</td>
      <td>29.0</td>
      <td>DEPARTMENT OF REVENUE</td>
      <td>1005</td>
      <td>2003.0</td>
      <td>Department of Revenue</td>
      <td>3157.0</td>
      <td>Street Operations</td>
      <td>7482</td>
      <td>Parking Enforcement Aide</td>
      <td>Monthly</td>
      <td>1272</td>
      <td>2944.0</td>
      <td>3744768.0</td>
    </tr>
    <tr>
      <th>1579</th>
      <td>2011</td>
      <td>Local</td>
      <td>100</td>
      <td>CORPORATE FUND</td>
      <td>38.0</td>
      <td>GENERAL SERVICES</td>
      <td>1005</td>
      <td>2125.0</td>
      <td>Bureau Trades and Engineering Management</td>
      <td>3182.0</td>
      <td>Building Engineering</td>
      <td>7747</td>
      <td>Chief Operating Engineer</td>
      <td>Monthly</td>
      <td>5</td>
      <td>8698.0</td>
      <td>521872.0</td>
    </tr>
    <tr>
      <th>1587</th>
      <td>2011</td>
      <td>Local</td>
      <td>100</td>
      <td>CORPORATE FUND</td>
      <td>38.0</td>
      <td>GENERAL SERVICES</td>
      <td>1005</td>
      <td>2125.0</td>
      <td>Bureau Trades and Engineering Management</td>
      <td>3183.0</td>
      <td>Trade Services</td>
      <td>4526</td>
      <td>General Foreman of General Trades</td>
      <td>Monthly</td>
      <td>2</td>
      <td>8713.0</td>
      <td>209123.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# List of departments
depts = dep_count.index

# loop through monthly salaried employee datafrome by year
for year in years:
    
    # Create a dataframe for a specific year
    mby_df = monthly_df.loc[monthly_df["year"] == year, :]
    
    # empty list to hold yearly monthly employee counts for a given year
    mby_list = []
    
    # loop through city departments
    for department in depts:
        
        # Create a dataframe for a specific department
        mby_dept_df = mby_df.loc[mby_df["department_description"] == department, :]
        
        # empty list to hold department employee counts
        mbd_list = []
        
        # loop through the rows for a given department
        for x in range(0, len(mby_dept_df)):
            
            # some of the data given is in 12 months increments per employee which is evident by the following:
            # total_budgeted_unit = 24; budgeted_pay_rate = 2298; total_budgeted_amount = 55152
            # this if statement appends that data
            if mby_dept_df.iloc[x, 14] * (mby_dept_df.iloc[x, 15] + 5) > mby_dept_df.iloc[x, 16]:
                
                mbd_list.append(mby_dept_df.iloc[x, 14]/12)
            
            # some of the data is given as number of employees which is evident by the the following:
            # total_budgeted_unit = 2; budgeted_pay_rate = 8713; total_budgeted_amount = 209123
            # the number of months per year (12) must be manually applied: 2 * 12 * 8713 = 209123
            # this else statement appends that data
            else:
                
                mbd_list.append(mby_dept_df.iloc[x, 14])
                
        # sum the employee numbers appended in the conditional statement above
        mby_list.append(sum(mbd_list))
    
    # Append the yearly monthly salaried employee data to the overall dataframe
    dep_count.loc[:, f"{year} Dept Monthly Employees"] = mby_list
```

### Find the number of employees paid hourly 

- per year
- per department


```python
# Pull hourly salaried employees into a dataframe
hourly_df = budget_by_year_df.loc[budget_by_year_df["budgeted_unit"] == "Hourly", :]
hourly_df.head()
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
      <th>189</th>
      <td>2011</td>
      <td>Local</td>
      <td>100</td>
      <td>CORPORATE FUND</td>
      <td>5.0</td>
      <td>OFFICE OF BUDGET &amp; MANAGEMENT</td>
      <td>1005</td>
      <td>2005.0</td>
      <td>Office of Budget and Management</td>
      <td>3035.0</td>
      <td>Return to Work</td>
      <td>6344</td>
      <td>Watchman - TRTW</td>
      <td>Hourly</td>
      <td>0</td>
      <td>19.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>266</th>
      <td>2011</td>
      <td>Local</td>
      <td>100</td>
      <td>CORPORATE FUND</td>
      <td>6.0</td>
      <td>DEPARTMENT OF INNOVATION &amp; TECHNOLOGY</td>
      <td>1005</td>
      <td>2005.0</td>
      <td>Department of Innovation and Technology</td>
      <td>3140.0</td>
      <td>Technical Operations</td>
      <td>5035</td>
      <td>Electrical Mechanic</td>
      <td>Hourly</td>
      <td>0</td>
      <td>40.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>795</th>
      <td>2011</td>
      <td>Local</td>
      <td>100</td>
      <td>CORPORATE FUND</td>
      <td>29.0</td>
      <td>DEPARTMENT OF REVENUE</td>
      <td>1005</td>
      <td>2003.0</td>
      <td>Department of Revenue</td>
      <td>3157.0</td>
      <td>Street Operations</td>
      <td>7112</td>
      <td>Booter - Parking</td>
      <td>Hourly</td>
      <td>20800</td>
      <td>30.0</td>
      <td>634400.0</td>
    </tr>
    <tr>
      <th>796</th>
      <td>2011</td>
      <td>Local</td>
      <td>100</td>
      <td>CORPORATE FUND</td>
      <td>29.0</td>
      <td>DEPARTMENT OF REVENUE</td>
      <td>1005</td>
      <td>2003.0</td>
      <td>Department of Revenue</td>
      <td>3157.0</td>
      <td>Street Operations</td>
      <td>7112</td>
      <td>Booter - Parking</td>
      <td>Hourly</td>
      <td>30</td>
      <td>30.0</td>
      <td>1903200.0</td>
    </tr>
    <tr>
      <th>797</th>
      <td>2011</td>
      <td>Local</td>
      <td>100</td>
      <td>CORPORATE FUND</td>
      <td>29.0</td>
      <td>DEPARTMENT OF REVENUE</td>
      <td>1005</td>
      <td>2003.0</td>
      <td>Department of Revenue</td>
      <td>3157.0</td>
      <td>Street Operations</td>
      <td>7113</td>
      <td>Supervising Booter - Parking</td>
      <td>Hourly</td>
      <td>5</td>
      <td>32.0</td>
      <td>328328.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# loop through hourly salaried employee datafrome by year
for year in years:
    
    # Create a dataframe for a specific year
    hby_df = hourly_df.loc[hourly_df["year"] == year, :]
    
    # empty list to hold yearly hourly employee counts for a given year
    hby_list = []
    
    # loop through city departments
    for department in depts:
        
        # Create a dataframe for a specific department
        hby_dept_df = hby_df.loc[hby_df["department_description"] == department, :]
        
        # empty list to hold department employee counts
        hbd_list = [] 
        
        # loop through the rows for a given department
        for x in range(0, len(hby_dept_df)):
            
            # confirm that the total budget ammount does not equal zero
            if hby_dept_df.iloc[x, 16] != 0:
                
                # some of the data given is in total number of hours per year
                # when this occurs, this statement estimates the number of employees by dividing by 2100 hrs/year and rounding up
                # if total_budgeted_unit * (budgeted_pay_rate + 5 (buffer for rounding)) > total_budgeted_amount
                # note that 2100 hrs/year is assumed to be an approximation of what the departments use
                # based on a calculated sample of the data
                if hby_dept_df.iloc[x, 14] * (hby_dept_df.iloc[x, 15] + 5) > hby_dept_df.iloc[x, 16]:
                    
                    hbd_list.append(int(round(hby_dept_df.iloc[x, 14]/2100)))
                
                # some of the data is given as number of employees
                # this statement appends those values
                else:
                    
                    hbd_list.append(hby_dept_df.iloc[x, 14])
                    
        # sum the employee numbers appended in the conditional statement above
        hby_list.append(sum(hbd_list))
    
    # Append the yearly monthly salaried employee data to the overall dataframe
    dep_count.loc[:, f"{year} Dept Hourly Employees"] = hby_list
```

## Summarize Employee Data


```python
# remove null values ("NaN")
for year in years:
    dep_count[f"{year} Dept Annual Employees"].fillna(0, inplace=True)
    
# sum total employees per year and append to dataframe
for year in years:
    dep_count.loc[:, f"{year} Dept Total Employees"] = dep_count[f"{year} Dept Annual Employees"] + \
                                                      dep_count[f"{year} Dept Monthly Employees"] + \
                                                     dep_count[f"{year} Dept Hourly Employees"]

# write the dataframe to a csv
dep_count.to_csv("dep_count.csv", index=True)

# Print the employee count dataframe
dep_count.head()
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
      <th>2011 Dept Annual Employees</th>
      <th>2012 Dept Annual Employees</th>
      <th>2013 Dept Annual Employees</th>
      <th>2014 Dept Annual Employees</th>
      <th>2015 Dept Annual Employees</th>
      <th>2016 Dept Annual Employees</th>
      <th>2017 Dept Annual Employees</th>
      <th>2011 Dept Monthly Employees</th>
      <th>2012 Dept Monthly Employees</th>
      <th>2013 Dept Monthly Employees</th>
      <th>...</th>
      <th>2015 Dept Hourly Employees</th>
      <th>2016 Dept Hourly Employees</th>
      <th>2017 Dept Hourly Employees</th>
      <th>2011 Dept Total Employees</th>
      <th>2012 Dept Total Employees</th>
      <th>2013 Dept Total Employees</th>
      <th>2014 Dept Total Employees</th>
      <th>2015 Dept Total Employees</th>
      <th>2016 Dept Total Employees</th>
      <th>2017 Dept Total Employees</th>
    </tr>
    <tr>
      <th>department_description</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BOARD OF ELECTION COMMISSIONER</th>
      <td>124</td>
      <td>124.0</td>
      <td>119.0</td>
      <td>118.0</td>
      <td>118.0</td>
      <td>118.0</td>
      <td>118.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>124.0</td>
      <td>124.0</td>
      <td>119.0</td>
      <td>118.0</td>
      <td>118.0</td>
      <td>118.0</td>
      <td>118.0</td>
    </tr>
    <tr>
      <th>BOARD OF ETHICS</th>
      <td>7</td>
      <td>8.0</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>8.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>7.0</td>
      <td>8.0</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>BUSINESS AFFAIRS AND CONSUMER PROTECTION</th>
      <td>196</td>
      <td>180.0</td>
      <td>187.0</td>
      <td>186.0</td>
      <td>186.0</td>
      <td>188.0</td>
      <td>189.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>203.0</td>
      <td>187.0</td>
      <td>194.0</td>
      <td>191.0</td>
      <td>191.0</td>
      <td>193.0</td>
      <td>194.0</td>
    </tr>
    <tr>
      <th>CHICAGO DEPT OF TRANSPORTATION</th>
      <td>373</td>
      <td>348.0</td>
      <td>360.0</td>
      <td>361.0</td>
      <td>359.0</td>
      <td>371.0</td>
      <td>376.0</td>
      <td>85.0</td>
      <td>78.0</td>
      <td>78.0</td>
      <td>...</td>
      <td>844</td>
      <td>857</td>
      <td>890</td>
      <td>979.0</td>
      <td>930.0</td>
      <td>932.0</td>
      <td>1170.0</td>
      <td>1296.0</td>
      <td>1320.0</td>
      <td>1361.0</td>
    </tr>
    <tr>
      <th>CHICAGO PUBLIC LIBRARY</th>
      <td>931</td>
      <td>786.0</td>
      <td>771.0</td>
      <td>775.0</td>
      <td>779.0</td>
      <td>794.0</td>
      <td>786.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>160</td>
      <td>157</td>
      <td>158</td>
      <td>1126.0</td>
      <td>831.0</td>
      <td>903.0</td>
      <td>934.0</td>
      <td>939.0</td>
      <td>951.0</td>
      <td>944.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 28 columns</p>
</div>




```python
# Summarize total employee counts in a dataframe
total_dep_emp = dep_count[["2011 Dept Total Employees", "2012 Dept Total Employees", "2013 Dept Total Employees", \
                          "2014 Dept Total Employees", "2015 Dept Total Employees", "2016 Dept Total Employees", \
                          "2017 Dept Total Employees"]]

# write the dataframe to a csv
total_dep_emp.to_csv("total_dep_emp.csv", index=True)

# print the dataframe
total_dep_emp
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
      <th>2011 Dept Total Employees</th>
      <th>2012 Dept Total Employees</th>
      <th>2013 Dept Total Employees</th>
      <th>2014 Dept Total Employees</th>
      <th>2015 Dept Total Employees</th>
      <th>2016 Dept Total Employees</th>
      <th>2017 Dept Total Employees</th>
    </tr>
    <tr>
      <th>department_description</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BOARD OF ELECTION COMMISSIONER</th>
      <td>124.000000</td>
      <td>124.0</td>
      <td>119.0</td>
      <td>118.0</td>
      <td>118.0</td>
      <td>118.0</td>
      <td>118.0</td>
    </tr>
    <tr>
      <th>BOARD OF ETHICS</th>
      <td>7.000000</td>
      <td>8.0</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>BUSINESS AFFAIRS AND CONSUMER PROTECTION</th>
      <td>203.000000</td>
      <td>187.0</td>
      <td>194.0</td>
      <td>191.0</td>
      <td>191.0</td>
      <td>193.0</td>
      <td>194.0</td>
    </tr>
    <tr>
      <th>CHICAGO DEPT OF TRANSPORTATION</th>
      <td>979.000000</td>
      <td>930.0</td>
      <td>932.0</td>
      <td>1170.0</td>
      <td>1296.0</td>
      <td>1320.0</td>
      <td>1361.0</td>
    </tr>
    <tr>
      <th>CHICAGO PUBLIC LIBRARY</th>
      <td>1126.000000</td>
      <td>831.0</td>
      <td>903.0</td>
      <td>934.0</td>
      <td>939.0</td>
      <td>951.0</td>
      <td>944.0</td>
    </tr>
    <tr>
      <th>CITY CLERK</th>
      <td>108.000000</td>
      <td>100.0</td>
      <td>98.0</td>
      <td>98.0</td>
      <td>96.0</td>
      <td>96.0</td>
      <td>96.0</td>
    </tr>
    <tr>
      <th>CITY COUNCIL</th>
      <td>234.000000</td>
      <td>236.0</td>
      <td>236.0</td>
      <td>240.0</td>
      <td>240.0</td>
      <td>239.0</td>
      <td>239.0</td>
    </tr>
    <tr>
      <th>CITY TREASURER</th>
      <td>22.000000</td>
      <td>23.0</td>
      <td>23.0</td>
      <td>24.0</td>
      <td>24.0</td>
      <td>32.0</td>
      <td>31.0</td>
    </tr>
    <tr>
      <th>COMM ANIMAL CARE AND CONTROL</th>
      <td>83.000000</td>
      <td>65.0</td>
      <td>81.0</td>
      <td>81.0</td>
      <td>82.0</td>
      <td>82.0</td>
      <td>86.0</td>
    </tr>
    <tr>
      <th>COMMISSION ON HUMAN RELATIONS</th>
      <td>33.000000</td>
      <td>21.0</td>
      <td>20.0</td>
      <td>20.0</td>
      <td>20.0</td>
      <td>20.0</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>CULTURAL AFFAIRS SPECIAL EVENT</th>
      <td>79.000000</td>
      <td>80.0</td>
      <td>80.0</td>
      <td>80.0</td>
      <td>81.0</td>
      <td>77.0</td>
      <td>77.0</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF AVIATION</th>
      <td>1451.000000</td>
      <td>1390.0</td>
      <td>1396.0</td>
      <td>1537.0</td>
      <td>1495.0</td>
      <td>1541.0</td>
      <td>1761.0</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF ENVIRONMENT</th>
      <td>82.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF FINANCE</th>
      <td>200.000000</td>
      <td>660.0</td>
      <td>627.0</td>
      <td>650.0</td>
      <td>655.0</td>
      <td>671.0</td>
      <td>667.0</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF FLEET MANAGEMENT</th>
      <td>673.000000</td>
      <td>1098.0</td>
      <td>1063.0</td>
      <td>1074.0</td>
      <td>1086.0</td>
      <td>1100.0</td>
      <td>1105.0</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF HUMAN RESOURCES</th>
      <td>79.000000</td>
      <td>75.0</td>
      <td>76.0</td>
      <td>76.0</td>
      <td>75.0</td>
      <td>77.0</td>
      <td>84.0</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF INNOVATION &amp; TECHNOLOGY</th>
      <td>96.000000</td>
      <td>90.0</td>
      <td>108.0</td>
      <td>110.0</td>
      <td>121.0</td>
      <td>118.0</td>
      <td>119.0</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF LAW</th>
      <td>431.000000</td>
      <td>424.0</td>
      <td>427.0</td>
      <td>437.0</td>
      <td>437.0</td>
      <td>436.0</td>
      <td>442.0</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF POLICE</th>
      <td>15718.000000</td>
      <td>14349.0</td>
      <td>14356.0</td>
      <td>14397.0</td>
      <td>14417.0</td>
      <td>13792.0</td>
      <td>14274.0</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF PROCUREMENT SERV</th>
      <td>76.000000</td>
      <td>83.0</td>
      <td>86.0</td>
      <td>90.0</td>
      <td>91.0</td>
      <td>91.0</td>
      <td>102.0</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF PUBLIC HEALTH</th>
      <td>1003.000000</td>
      <td>905.0</td>
      <td>748.0</td>
      <td>724.0</td>
      <td>668.0</td>
      <td>614.0</td>
      <td>606.0</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF REVENUE</th>
      <td>467.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>DEPT OF ADMINISTRATIVE HEARING</th>
      <td>44.000000</td>
      <td>41.0</td>
      <td>42.0</td>
      <td>42.0</td>
      <td>42.0</td>
      <td>42.0</td>
      <td>42.0</td>
    </tr>
    <tr>
      <th>DEPT OF BUILDINGS</th>
      <td>322.000000</td>
      <td>274.0</td>
      <td>285.0</td>
      <td>288.0</td>
      <td>289.0</td>
      <td>287.0</td>
      <td>294.0</td>
    </tr>
    <tr>
      <th>DEPT OF WATER MANAGEMENT</th>
      <td>2198.000000</td>
      <td>2130.0</td>
      <td>2131.0</td>
      <td>2138.0</td>
      <td>2139.0</td>
      <td>2129.0</td>
      <td>2282.0</td>
    </tr>
    <tr>
      <th>DEPT STREETS AND SANITATION</th>
      <td>2569.000000</td>
      <td>2300.0</td>
      <td>2349.0</td>
      <td>2339.0</td>
      <td>2339.0</td>
      <td>2326.0</td>
      <td>2296.0</td>
    </tr>
    <tr>
      <th>FAMILY AND SUPPORT SERVICES</th>
      <td>845.083333</td>
      <td>656.0</td>
      <td>564.0</td>
      <td>541.0</td>
      <td>516.0</td>
      <td>403.0</td>
      <td>402.0</td>
    </tr>
    <tr>
      <th>FIRE DEPARTMENT</th>
      <td>5180.000000</td>
      <td>5143.0</td>
      <td>5142.0</td>
      <td>5162.0</td>
      <td>5185.0</td>
      <td>5171.0</td>
      <td>5173.0</td>
    </tr>
    <tr>
      <th>GENERAL SERVICES</th>
      <td>455.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>HOUSING AND ECONOMIC DEVELOPMT</th>
      <td>242.000000</td>
      <td>240.0</td>
      <td>227.0</td>
      <td>227.0</td>
      <td>228.0</td>
      <td>229.0</td>
      <td>230.0</td>
    </tr>
    <tr>
      <th>INDEPENDENT POLICE REVIEW AUTHORITY</th>
      <td>97.000000</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>98.0</td>
      <td>97.0</td>
      <td>62.0</td>
    </tr>
    <tr>
      <th>INSPECTOR GENERAL</th>
      <td>71.000000</td>
      <td>67.0</td>
      <td>67.0</td>
      <td>65.0</td>
      <td>67.0</td>
      <td>64.0</td>
      <td>96.0</td>
    </tr>
    <tr>
      <th>LICENSE APPEAL COMMISSION</th>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>MAYORS OFFICE-DISABILITIES</th>
      <td>34.000000</td>
      <td>32.0</td>
      <td>31.0</td>
      <td>30.0</td>
      <td>30.0</td>
      <td>29.0</td>
      <td>29.0</td>
    </tr>
    <tr>
      <th>OFFICE OF BUDGET &amp; MANAGEMENT</th>
      <td>43.000000</td>
      <td>38.0</td>
      <td>40.0</td>
      <td>44.0</td>
      <td>42.0</td>
      <td>45.0</td>
      <td>50.0</td>
    </tr>
    <tr>
      <th>OFFICE OF COMPLIANCE</th>
      <td>33.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>OFFICE OF EMERGENCY MANAGEMENT &amp; COMMUNICATIONS</th>
      <td>1120.000000</td>
      <td>922.0</td>
      <td>918.0</td>
      <td>928.0</td>
      <td>928.0</td>
      <td>1844.0</td>
      <td>2135.0</td>
    </tr>
    <tr>
      <th>OFFICE OF THE MAYOR</th>
      <td>78.000000</td>
      <td>83.0</td>
      <td>86.0</td>
      <td>88.0</td>
      <td>91.0</td>
      <td>80.0</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>POLICE BOARD</th>
      <td>2.000000</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>



## Summarize Budget Data

- per year
- per department
- department budget changes between 2011 and 2017


```python
#empty dataframe to append department budget data to
dep_budgets = pd.DataFrame()

# Loop to add yearly department budgets to the empty dataframe
for year in years:
    
    # Create a dataframe for a specific year
    year_df = budget_by_year_df.loc[budget_by_year_df["year"] == year, :]
    
    # Create a groupby object based on department
    year_gp = year_df.groupby("department_description")
    
    # Sum the budgets per department
    year_dep_budget = year_gp["total_budgeted_amount"].sum()
    
    # append to the budget datafrome
    dep_budgets.loc[:, f"{year} Dept Budgets"] = year_dep_budget
```


```python
# make sure all data is an integer and remove null values ("NaN")
for year in years:
    dep_budgets[f"{year} Dept Budgets"].fillna(0, inplace=True)
    dep_budgets[f"{year} Dept Budgets"] = dep_budgets[f"{year} Dept Budgets"].astype(int)
```


```python
# write the dataframe to a csv
dep_budgets.to_csv("dep_budgets.csv", index=True)

# print the yearly department budgets
dep_budgets
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
      <th>2011 Dept Budgets</th>
      <th>2012 Dept Budgets</th>
      <th>2013 Dept Budgets</th>
      <th>2014 Dept Budgets</th>
      <th>2015 Dept Budgets</th>
      <th>2016 Dept Budgets</th>
      <th>2017 Dept Budgets</th>
    </tr>
    <tr>
      <th>department_description</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BOARD OF ELECTION COMMISSIONER</th>
      <td>7164438</td>
      <td>7090200</td>
      <td>6975224</td>
      <td>6698976</td>
      <td>6640056</td>
      <td>6675516</td>
      <td>6691812</td>
    </tr>
    <tr>
      <th>BOARD OF ETHICS</th>
      <td>564692</td>
      <td>684372</td>
      <td>734856</td>
      <td>743398</td>
      <td>753920</td>
      <td>782762</td>
      <td>756420</td>
    </tr>
    <tr>
      <th>BUSINESS AFFAIRS AND CONSUMER PROTECTION</th>
      <td>14289454</td>
      <td>13327564</td>
      <td>14196494</td>
      <td>14021036</td>
      <td>14372441</td>
      <td>14862470</td>
      <td>15133494</td>
    </tr>
    <tr>
      <th>CHICAGO DEPT OF TRANSPORTATION</th>
      <td>77050619</td>
      <td>73640928</td>
      <td>75058393</td>
      <td>95084744</td>
      <td>107712427</td>
      <td>112111198</td>
      <td>117872199</td>
    </tr>
    <tr>
      <th>CHICAGO PUBLIC LIBRARY</th>
      <td>61214529</td>
      <td>52478537</td>
      <td>56264419</td>
      <td>56957264</td>
      <td>60123787</td>
      <td>61919246</td>
      <td>62347380</td>
    </tr>
    <tr>
      <th>CITY CLERK</th>
      <td>6495095</td>
      <td>6224565</td>
      <td>6196686</td>
      <td>6184130</td>
      <td>6483725</td>
      <td>6548579</td>
      <td>6638313</td>
    </tr>
    <tr>
      <th>CITY COUNCIL</th>
      <td>7779701</td>
      <td>7951243</td>
      <td>8015890</td>
      <td>8286567</td>
      <td>8375445</td>
      <td>8370000</td>
      <td>8397702</td>
    </tr>
    <tr>
      <th>CITY TREASURER</th>
      <td>1797986</td>
      <td>1915707</td>
      <td>1945556</td>
      <td>2034370</td>
      <td>2071902</td>
      <td>2735667</td>
      <td>2705379</td>
    </tr>
    <tr>
      <th>COMM ANIMAL CARE AND CONTROL</th>
      <td>4253807</td>
      <td>3764004</td>
      <td>4107943</td>
      <td>4189165</td>
      <td>4406031</td>
      <td>4507966</td>
      <td>4707068</td>
    </tr>
    <tr>
      <th>COMMISSION ON HUMAN RELATIONS</th>
      <td>2693324</td>
      <td>1822644</td>
      <td>1978076</td>
      <td>1954763</td>
      <td>2022154</td>
      <td>2094141</td>
      <td>2137901</td>
    </tr>
    <tr>
      <th>CULTURAL AFFAIRS SPECIAL EVENT</th>
      <td>6377498</td>
      <td>6417376</td>
      <td>6524740</td>
      <td>6595724</td>
      <td>6615853</td>
      <td>6579828</td>
      <td>6678326</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF AVIATION</th>
      <td>98632794</td>
      <td>95781375</td>
      <td>99299050</td>
      <td>107906361</td>
      <td>108351113</td>
      <td>114660998</td>
      <td>132831842</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF ENVIRONMENT</th>
      <td>6252016</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF FINANCE</th>
      <td>15480967</td>
      <td>42561051</td>
      <td>41586903</td>
      <td>42453071</td>
      <td>43729711</td>
      <td>45743945</td>
      <td>46117011</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF FLEET MANAGEMENT</th>
      <td>51980691</td>
      <td>82725994</td>
      <td>85956838</td>
      <td>87284749</td>
      <td>89100697</td>
      <td>92187397</td>
      <td>94179766</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF HUMAN RESOURCES</th>
      <td>5639178</td>
      <td>5163670</td>
      <td>5281912</td>
      <td>5458543</td>
      <td>5459257</td>
      <td>5791194</td>
      <td>6445182</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF INNOVATION &amp; TECHNOLOGY</th>
      <td>8899572</td>
      <td>8458776</td>
      <td>10549678</td>
      <td>10658813</td>
      <td>11984346</td>
      <td>11889722</td>
      <td>12244598</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF LAW</th>
      <td>33819276</td>
      <td>33443990</td>
      <td>33790039</td>
      <td>33847180</td>
      <td>34088165</td>
      <td>34643728</td>
      <td>35571731</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF POLICE</th>
      <td>1160612152</td>
      <td>1097282591</td>
      <td>1090086989</td>
      <td>1090429867</td>
      <td>1174521818</td>
      <td>1189619470</td>
      <td>1219409661</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF PROCUREMENT SERV</th>
      <td>5944492</td>
      <td>6322552</td>
      <td>6609250</td>
      <td>6904168</td>
      <td>7045905</td>
      <td>7263853</td>
      <td>8164835</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF PUBLIC HEALTH</th>
      <td>71216838</td>
      <td>65376928</td>
      <td>70926941</td>
      <td>69010744</td>
      <td>65243235</td>
      <td>64063882</td>
      <td>64476642</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF REVENUE</th>
      <td>27225547</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>DEPT OF ADMINISTRATIVE HEARING</th>
      <td>2995132</td>
      <td>2823792</td>
      <td>2916091</td>
      <td>2987155</td>
      <td>3054174</td>
      <td>3131339</td>
      <td>3226372</td>
    </tr>
    <tr>
      <th>DEPT OF BUILDINGS</th>
      <td>27793781</td>
      <td>24506192</td>
      <td>27677689</td>
      <td>28013176</td>
      <td>28795733</td>
      <td>29577697</td>
      <td>31023166</td>
    </tr>
    <tr>
      <th>DEPT OF WATER MANAGEMENT</th>
      <td>173719856</td>
      <td>170134420</td>
      <td>174961431</td>
      <td>178245160</td>
      <td>182865079</td>
      <td>185994418</td>
      <td>197359104</td>
    </tr>
    <tr>
      <th>DEPT STREETS AND SANITATION</th>
      <td>171978017</td>
      <td>158312618</td>
      <td>165449712</td>
      <td>168429738</td>
      <td>167649417</td>
      <td>167949788</td>
      <td>167016513</td>
    </tr>
    <tr>
      <th>FAMILY AND SUPPORT SERVICES</th>
      <td>43587190</td>
      <td>36096416</td>
      <td>41986556</td>
      <td>40050030</td>
      <td>38373858</td>
      <td>38752405</td>
      <td>39597556</td>
    </tr>
    <tr>
      <th>FIRE DEPARTMENT</th>
      <td>415494038</td>
      <td>456287445</td>
      <td>458891612</td>
      <td>456297642</td>
      <td>487176453</td>
      <td>501411942</td>
      <td>507495453</td>
    </tr>
    <tr>
      <th>GENERAL SERVICES</th>
      <td>32296581</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>HOUSING AND ECONOMIC DEVELOPMT</th>
      <td>19515395</td>
      <td>19564290</td>
      <td>20898062</td>
      <td>20804680</td>
      <td>21139346</td>
      <td>22165818</td>
      <td>22361417</td>
    </tr>
    <tr>
      <th>INDEPENDENT POLICE REVIEW AUTHORITY</th>
      <td>7561508</td>
      <td>7810032</td>
      <td>7973938</td>
      <td>8076223</td>
      <td>8378945</td>
      <td>8413479</td>
      <td>5712646</td>
    </tr>
    <tr>
      <th>INSPECTOR GENERAL</th>
      <td>5553703</td>
      <td>5083608</td>
      <td>5171189</td>
      <td>5061998</td>
      <td>5220196</td>
      <td>5320584</td>
      <td>7707759</td>
    </tr>
    <tr>
      <th>LICENSE APPEAL COMMISSION</th>
      <td>63276</td>
      <td>63276</td>
      <td>65169</td>
      <td>65436</td>
      <td>67017</td>
      <td>74045</td>
      <td>76932</td>
    </tr>
    <tr>
      <th>MAYORS OFFICE-DISABILITIES</th>
      <td>2514605</td>
      <td>2349612</td>
      <td>2835670</td>
      <td>2759694</td>
      <td>2790730</td>
      <td>2855215</td>
      <td>2889139</td>
    </tr>
    <tr>
      <th>OFFICE OF BUDGET &amp; MANAGEMENT</th>
      <td>3885581</td>
      <td>3325176</td>
      <td>4074826</td>
      <td>4453611</td>
      <td>4164548</td>
      <td>4503344</td>
      <td>5119568</td>
    </tr>
    <tr>
      <th>OFFICE OF COMPLIANCE</th>
      <td>2676780</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>OFFICE OF EMERGENCY MANAGEMENT &amp; COMMUNICATIONS</th>
      <td>72760175</td>
      <td>61780680</td>
      <td>62951692</td>
      <td>65110197</td>
      <td>66420070</td>
      <td>81346205</td>
      <td>96261836</td>
    </tr>
    <tr>
      <th>OFFICE OF THE MAYOR</th>
      <td>6560814</td>
      <td>7118412</td>
      <td>7835395</td>
      <td>8153775</td>
      <td>8490091</td>
      <td>7509920</td>
      <td>7672804</td>
    </tr>
    <tr>
      <th>POLICE BOARD</th>
      <td>155376</td>
      <td>155376</td>
      <td>157906</td>
      <td>158136</td>
      <td>158136</td>
      <td>162577</td>
      <td>172272</td>
    </tr>
  </tbody>
</table>
</div>




```python
# empty list to append budget changes
budget_changes = []

# list of departments for the dataframe
departments = dep_budgets.index

# Calculate department budget changes between 2011 and 2017
for x in range(0, len(dep_budgets)):
    diff = dep_budgets.iloc[x, 6] - dep_budgets.iloc[x, 0]
    budget_changes.append(diff)
    
# create a dataframe for the budget changes 
diff_budgets = pd.DataFrame({"Departments": departments,
                            "Budget Changes": budget_changes})
```


```python
# save a sorted version of the dataframe
diff_budgets_sorted = diff_budgets[["Departments", "Budget Changes"]]
diff_budgets_sorted = diff_budgets_sorted.sort_values('Budget Changes', ascending=False)

# reset the index and print the dataframe
diff_budgets_sorted = diff_budgets_sorted.set_index("Departments")

# write the dataframe to a csv
diff_budgets_sorted.to_csv("diff_budgets_sorted.csv", index=True)

diff_budgets_sorted
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
      <th>Budget Changes</th>
    </tr>
    <tr>
      <th>Departments</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>FIRE DEPARTMENT</th>
      <td>92001415</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF POLICE</th>
      <td>58797509</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF FLEET MANAGEMENT</th>
      <td>42199075</td>
    </tr>
    <tr>
      <th>CHICAGO DEPT OF TRANSPORTATION</th>
      <td>40821580</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF AVIATION</th>
      <td>34199048</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF FINANCE</th>
      <td>30636044</td>
    </tr>
    <tr>
      <th>DEPT OF WATER MANAGEMENT</th>
      <td>23639248</td>
    </tr>
    <tr>
      <th>OFFICE OF EMERGENCY MANAGEMENT &amp; COMMUNICATIONS</th>
      <td>23501661</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF INNOVATION &amp; TECHNOLOGY</th>
      <td>3345026</td>
    </tr>
    <tr>
      <th>DEPT OF BUILDINGS</th>
      <td>3229385</td>
    </tr>
    <tr>
      <th>HOUSING AND ECONOMIC DEVELOPMT</th>
      <td>2846022</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF PROCUREMENT SERV</th>
      <td>2220343</td>
    </tr>
    <tr>
      <th>INSPECTOR GENERAL</th>
      <td>2154056</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF LAW</th>
      <td>1752455</td>
    </tr>
    <tr>
      <th>OFFICE OF BUDGET &amp; MANAGEMENT</th>
      <td>1233987</td>
    </tr>
    <tr>
      <th>CHICAGO PUBLIC LIBRARY</th>
      <td>1132851</td>
    </tr>
    <tr>
      <th>OFFICE OF THE MAYOR</th>
      <td>1111990</td>
    </tr>
    <tr>
      <th>CITY TREASURER</th>
      <td>907393</td>
    </tr>
    <tr>
      <th>BUSINESS AFFAIRS AND CONSUMER PROTECTION</th>
      <td>844040</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF HUMAN RESOURCES</th>
      <td>806004</td>
    </tr>
    <tr>
      <th>CITY COUNCIL</th>
      <td>618001</td>
    </tr>
    <tr>
      <th>COMM ANIMAL CARE AND CONTROL</th>
      <td>453261</td>
    </tr>
    <tr>
      <th>MAYORS OFFICE-DISABILITIES</th>
      <td>374534</td>
    </tr>
    <tr>
      <th>CULTURAL AFFAIRS SPECIAL EVENT</th>
      <td>300828</td>
    </tr>
    <tr>
      <th>DEPT OF ADMINISTRATIVE HEARING</th>
      <td>231240</td>
    </tr>
    <tr>
      <th>BOARD OF ETHICS</th>
      <td>191728</td>
    </tr>
    <tr>
      <th>CITY CLERK</th>
      <td>143218</td>
    </tr>
    <tr>
      <th>POLICE BOARD</th>
      <td>16896</td>
    </tr>
    <tr>
      <th>LICENSE APPEAL COMMISSION</th>
      <td>13656</td>
    </tr>
    <tr>
      <th>BOARD OF ELECTION COMMISSIONER</th>
      <td>-472626</td>
    </tr>
    <tr>
      <th>COMMISSION ON HUMAN RELATIONS</th>
      <td>-555423</td>
    </tr>
    <tr>
      <th>INDEPENDENT POLICE REVIEW AUTHORITY</th>
      <td>-1848862</td>
    </tr>
    <tr>
      <th>OFFICE OF COMPLIANCE</th>
      <td>-2676780</td>
    </tr>
    <tr>
      <th>FAMILY AND SUPPORT SERVICES</th>
      <td>-3989634</td>
    </tr>
    <tr>
      <th>DEPT STREETS AND SANITATION</th>
      <td>-4961504</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF ENVIRONMENT</th>
      <td>-6252016</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF PUBLIC HEALTH</th>
      <td>-6740196</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF REVENUE</th>
      <td>-27225547</td>
    </tr>
    <tr>
      <th>GENERAL SERVICES</th>
      <td>-32296581</td>
    </tr>
  </tbody>
</table>
</div>



## Summarize Average Salary Data

- per year
- per department
- department salary changes between 2011 and 2017


```python
#empty dataframe to append department salary data to
dep_salaries = pd.DataFrame()

# Loop to add yearly department average salaries to the empty dataframe
for year in years:
    
    dep_salaries.loc[:, f"{year} Dept Avg Salary"] = round(dep_budgets[f"{year} Dept Budgets"]/total_dep_emp[f"{year} Dept Total Employees"],2)
    
```


```python
# make sure all data is an integer and remove null values ("NaN")
for year in years:
    dep_salaries[f"{year} Dept Avg Salary"].fillna(0, inplace=True)

# write the dataframe to a csv
dep_salaries.to_csv("dep_salaries.csv", index=True)
    
# print the department average salaries dataframe
dep_salaries
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
      <th>2011 Dept Avg Salary</th>
      <th>2012 Dept Avg Salary</th>
      <th>2013 Dept Avg Salary</th>
      <th>2014 Dept Avg Salary</th>
      <th>2015 Dept Avg Salary</th>
      <th>2016 Dept Avg Salary</th>
      <th>2017 Dept Avg Salary</th>
    </tr>
    <tr>
      <th>department_description</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BOARD OF ELECTION COMMISSIONER</th>
      <td>57777.73</td>
      <td>57179.03</td>
      <td>58615.33</td>
      <td>56770.98</td>
      <td>56271.66</td>
      <td>56572.17</td>
      <td>56710.27</td>
    </tr>
    <tr>
      <th>BOARD OF ETHICS</th>
      <td>80670.29</td>
      <td>85546.50</td>
      <td>81650.67</td>
      <td>82599.78</td>
      <td>83768.89</td>
      <td>86973.56</td>
      <td>94552.50</td>
    </tr>
    <tr>
      <th>BUSINESS AFFAIRS AND CONSUMER PROTECTION</th>
      <td>70391.40</td>
      <td>71270.40</td>
      <td>73177.80</td>
      <td>73408.57</td>
      <td>75248.38</td>
      <td>77007.62</td>
      <td>78007.70</td>
    </tr>
    <tr>
      <th>CHICAGO DEPT OF TRANSPORTATION</th>
      <td>78703.39</td>
      <td>79183.79</td>
      <td>80534.76</td>
      <td>81269.01</td>
      <td>83111.44</td>
      <td>84932.73</td>
      <td>86607.05</td>
    </tr>
    <tr>
      <th>CHICAGO PUBLIC LIBRARY</th>
      <td>54364.59</td>
      <td>63151.07</td>
      <td>62308.33</td>
      <td>60982.08</td>
      <td>64029.59</td>
      <td>65109.62</td>
      <td>66045.95</td>
    </tr>
    <tr>
      <th>CITY CLERK</th>
      <td>60139.77</td>
      <td>62245.65</td>
      <td>63231.49</td>
      <td>63103.37</td>
      <td>67538.80</td>
      <td>68214.36</td>
      <td>69149.09</td>
    </tr>
    <tr>
      <th>CITY COUNCIL</th>
      <td>33246.59</td>
      <td>33691.71</td>
      <td>33965.64</td>
      <td>34527.36</td>
      <td>34897.69</td>
      <td>35020.92</td>
      <td>35136.83</td>
    </tr>
    <tr>
      <th>CITY TREASURER</th>
      <td>81726.64</td>
      <td>83291.61</td>
      <td>84589.39</td>
      <td>84765.42</td>
      <td>86329.25</td>
      <td>85489.59</td>
      <td>87270.29</td>
    </tr>
    <tr>
      <th>COMM ANIMAL CARE AND CONTROL</th>
      <td>51250.69</td>
      <td>57907.75</td>
      <td>50715.35</td>
      <td>51718.09</td>
      <td>53732.09</td>
      <td>54975.20</td>
      <td>54733.35</td>
    </tr>
    <tr>
      <th>COMMISSION ON HUMAN RELATIONS</th>
      <td>81615.88</td>
      <td>86792.57</td>
      <td>98903.80</td>
      <td>97738.15</td>
      <td>101107.70</td>
      <td>104707.05</td>
      <td>106895.05</td>
    </tr>
    <tr>
      <th>CULTURAL AFFAIRS SPECIAL EVENT</th>
      <td>80727.82</td>
      <td>80217.20</td>
      <td>81559.25</td>
      <td>82446.55</td>
      <td>81677.20</td>
      <td>85452.31</td>
      <td>86731.51</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF AVIATION</th>
      <td>67975.74</td>
      <td>68907.46</td>
      <td>71131.12</td>
      <td>70205.83</td>
      <td>72475.66</td>
      <td>74406.88</td>
      <td>75429.78</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF ENVIRONMENT</th>
      <td>76244.10</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF FINANCE</th>
      <td>77404.84</td>
      <td>64486.44</td>
      <td>66326.80</td>
      <td>65312.42</td>
      <td>66762.92</td>
      <td>68172.79</td>
      <td>69140.95</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF FLEET MANAGEMENT</th>
      <td>77237.28</td>
      <td>75342.44</td>
      <td>80862.50</td>
      <td>81270.72</td>
      <td>82044.84</td>
      <td>83806.72</td>
      <td>85230.56</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF HUMAN RESOURCES</th>
      <td>71382.00</td>
      <td>68848.93</td>
      <td>69498.84</td>
      <td>71822.93</td>
      <td>72790.09</td>
      <td>75210.31</td>
      <td>76728.36</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF INNOVATION &amp; TECHNOLOGY</th>
      <td>92703.88</td>
      <td>93986.40</td>
      <td>97682.20</td>
      <td>96898.30</td>
      <td>99044.18</td>
      <td>100760.36</td>
      <td>102895.78</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF LAW</th>
      <td>78467.00</td>
      <td>78877.33</td>
      <td>79133.58</td>
      <td>77453.50</td>
      <td>78004.95</td>
      <td>79458.09</td>
      <td>80479.03</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF POLICE</th>
      <td>73839.68</td>
      <td>76471.01</td>
      <td>75932.50</td>
      <td>75740.08</td>
      <td>81467.84</td>
      <td>86254.31</td>
      <td>85428.73</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF PROCUREMENT SERV</th>
      <td>78217.00</td>
      <td>76175.33</td>
      <td>76851.74</td>
      <td>76712.98</td>
      <td>77427.53</td>
      <td>79822.56</td>
      <td>80047.40</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF PUBLIC HEALTH</th>
      <td>71003.83</td>
      <td>72239.70</td>
      <td>94822.11</td>
      <td>95318.71</td>
      <td>97669.51</td>
      <td>104338.57</td>
      <td>106397.10</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF REVENUE</th>
      <td>58298.82</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>DEPT OF ADMINISTRATIVE HEARING</th>
      <td>68071.18</td>
      <td>68872.98</td>
      <td>69430.74</td>
      <td>71122.74</td>
      <td>72718.43</td>
      <td>74555.69</td>
      <td>76818.38</td>
    </tr>
    <tr>
      <th>DEPT OF BUILDINGS</th>
      <td>86316.09</td>
      <td>89438.66</td>
      <td>97114.70</td>
      <td>97267.97</td>
      <td>99639.21</td>
      <td>103058.18</td>
      <td>105520.97</td>
    </tr>
    <tr>
      <th>DEPT OF WATER MANAGEMENT</th>
      <td>79035.42</td>
      <td>79875.31</td>
      <td>82102.97</td>
      <td>83370.05</td>
      <td>85490.92</td>
      <td>87362.34</td>
      <td>86485.15</td>
    </tr>
    <tr>
      <th>DEPT STREETS AND SANITATION</th>
      <td>66943.56</td>
      <td>68831.57</td>
      <td>70434.10</td>
      <td>72009.29</td>
      <td>71675.68</td>
      <td>72205.41</td>
      <td>72742.38</td>
    </tr>
    <tr>
      <th>FAMILY AND SUPPORT SERVICES</th>
      <td>51577.39</td>
      <td>55025.02</td>
      <td>74444.25</td>
      <td>74029.63</td>
      <td>74367.94</td>
      <td>96159.81</td>
      <td>98501.38</td>
    </tr>
    <tr>
      <th>FIRE DEPARTMENT</th>
      <td>80211.20</td>
      <td>88720.09</td>
      <td>89243.80</td>
      <td>88395.51</td>
      <td>93958.81</td>
      <td>96966.15</td>
      <td>98104.67</td>
    </tr>
    <tr>
      <th>GENERAL SERVICES</th>
      <td>70981.50</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>HOUSING AND ECONOMIC DEVELOPMT</th>
      <td>80642.13</td>
      <td>81517.88</td>
      <td>92061.95</td>
      <td>91650.57</td>
      <td>92716.43</td>
      <td>96793.97</td>
      <td>97223.55</td>
    </tr>
    <tr>
      <th>INDEPENDENT POLICE REVIEW AUTHORITY</th>
      <td>77953.69</td>
      <td>78889.21</td>
      <td>80544.83</td>
      <td>81578.01</td>
      <td>85499.44</td>
      <td>86736.90</td>
      <td>92139.45</td>
    </tr>
    <tr>
      <th>INSPECTOR GENERAL</th>
      <td>78221.17</td>
      <td>75874.75</td>
      <td>77181.93</td>
      <td>77876.89</td>
      <td>77913.37</td>
      <td>83134.12</td>
      <td>80289.16</td>
    </tr>
    <tr>
      <th>LICENSE APPEAL COMMISSION</th>
      <td>63276.00</td>
      <td>63276.00</td>
      <td>65169.00</td>
      <td>65436.00</td>
      <td>67017.00</td>
      <td>74045.00</td>
      <td>76932.00</td>
    </tr>
    <tr>
      <th>MAYORS OFFICE-DISABILITIES</th>
      <td>73958.97</td>
      <td>73425.38</td>
      <td>91473.23</td>
      <td>91989.80</td>
      <td>93024.33</td>
      <td>98455.69</td>
      <td>99625.48</td>
    </tr>
    <tr>
      <th>OFFICE OF BUDGET &amp; MANAGEMENT</th>
      <td>90362.35</td>
      <td>87504.63</td>
      <td>101870.65</td>
      <td>101218.43</td>
      <td>99155.90</td>
      <td>100074.31</td>
      <td>102391.36</td>
    </tr>
    <tr>
      <th>OFFICE OF COMPLIANCE</th>
      <td>81114.55</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>OFFICE OF EMERGENCY MANAGEMENT &amp; COMMUNICATIONS</th>
      <td>64964.44</td>
      <td>67007.25</td>
      <td>68574.83</td>
      <td>70161.85</td>
      <td>71573.35</td>
      <td>44113.99</td>
      <td>45087.51</td>
    </tr>
    <tr>
      <th>OFFICE OF THE MAYOR</th>
      <td>84113.00</td>
      <td>85764.00</td>
      <td>91109.24</td>
      <td>92656.53</td>
      <td>93297.70</td>
      <td>93874.00</td>
      <td>95910.05</td>
    </tr>
    <tr>
      <th>POLICE BOARD</th>
      <td>77688.00</td>
      <td>77688.00</td>
      <td>78953.00</td>
      <td>79068.00</td>
      <td>79068.00</td>
      <td>81288.50</td>
      <td>86136.00</td>
    </tr>
  </tbody>
</table>
</div>




```python
# empty list to append salary changes
salary_changes = []

# list of departments for the dataframe
departments = dep_salaries.index

# Calculate department salary changes between 2011 and 2017
for x in range(0, len(dep_budgets)):
    diff = dep_salaries.iloc[x, 6] - dep_salaries.iloc[x, 0]
    salary_changes.append(diff)
    
# create a dataframe for the salary changes
diff_salaries = pd.DataFrame({"Departments": departments,
                            "Salary Changes": salary_changes})  
```


```python
# save a sorted version of the dataframe
diff_salaries_sorted = diff_salaries[["Departments", "Salary Changes"]]
diff_salaries_sorted = diff_salaries_sorted.sort_values("Salary Changes", ascending=False)

# reset the index and print the dataframe
diff_salaries_sorted = diff_salaries_sorted.set_index("Departments")

# write the dataframe to a csv
diff_salaries_sorted.to_csv("diff_salaries_sorted.csv", index=True)

diff_salaries_sorted
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
      <th>Salary Changes</th>
    </tr>
    <tr>
      <th>Departments</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>FAMILY AND SUPPORT SERVICES</th>
      <td>46923.99</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF PUBLIC HEALTH</th>
      <td>35393.27</td>
    </tr>
    <tr>
      <th>MAYORS OFFICE-DISABILITIES</th>
      <td>25666.51</td>
    </tr>
    <tr>
      <th>COMMISSION ON HUMAN RELATIONS</th>
      <td>25279.17</td>
    </tr>
    <tr>
      <th>DEPT OF BUILDINGS</th>
      <td>19204.88</td>
    </tr>
    <tr>
      <th>FIRE DEPARTMENT</th>
      <td>17893.47</td>
    </tr>
    <tr>
      <th>HOUSING AND ECONOMIC DEVELOPMT</th>
      <td>16581.42</td>
    </tr>
    <tr>
      <th>INDEPENDENT POLICE REVIEW AUTHORITY</th>
      <td>14185.76</td>
    </tr>
    <tr>
      <th>BOARD OF ETHICS</th>
      <td>13882.21</td>
    </tr>
    <tr>
      <th>LICENSE APPEAL COMMISSION</th>
      <td>13656.00</td>
    </tr>
    <tr>
      <th>OFFICE OF BUDGET &amp; MANAGEMENT</th>
      <td>12029.01</td>
    </tr>
    <tr>
      <th>OFFICE OF THE MAYOR</th>
      <td>11797.05</td>
    </tr>
    <tr>
      <th>CHICAGO PUBLIC LIBRARY</th>
      <td>11681.36</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF POLICE</th>
      <td>11589.05</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF INNOVATION &amp; TECHNOLOGY</th>
      <td>10191.90</td>
    </tr>
    <tr>
      <th>CITY CLERK</th>
      <td>9009.32</td>
    </tr>
    <tr>
      <th>DEPT OF ADMINISTRATIVE HEARING</th>
      <td>8747.20</td>
    </tr>
    <tr>
      <th>POLICE BOARD</th>
      <td>8448.00</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF FLEET MANAGEMENT</th>
      <td>7993.28</td>
    </tr>
    <tr>
      <th>CHICAGO DEPT OF TRANSPORTATION</th>
      <td>7903.66</td>
    </tr>
    <tr>
      <th>BUSINESS AFFAIRS AND CONSUMER PROTECTION</th>
      <td>7616.30</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF AVIATION</th>
      <td>7454.04</td>
    </tr>
    <tr>
      <th>DEPT OF WATER MANAGEMENT</th>
      <td>7449.73</td>
    </tr>
    <tr>
      <th>CULTURAL AFFAIRS SPECIAL EVENT</th>
      <td>6003.69</td>
    </tr>
    <tr>
      <th>DEPT STREETS AND SANITATION</th>
      <td>5798.82</td>
    </tr>
    <tr>
      <th>CITY TREASURER</th>
      <td>5543.65</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF HUMAN RESOURCES</th>
      <td>5346.36</td>
    </tr>
    <tr>
      <th>COMM ANIMAL CARE AND CONTROL</th>
      <td>3482.66</td>
    </tr>
    <tr>
      <th>INSPECTOR GENERAL</th>
      <td>2067.99</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF LAW</th>
      <td>2012.03</td>
    </tr>
    <tr>
      <th>CITY COUNCIL</th>
      <td>1890.24</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF PROCUREMENT SERV</th>
      <td>1830.40</td>
    </tr>
    <tr>
      <th>BOARD OF ELECTION COMMISSIONER</th>
      <td>-1067.46</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF FINANCE</th>
      <td>-8263.89</td>
    </tr>
    <tr>
      <th>OFFICE OF EMERGENCY MANAGEMENT &amp; COMMUNICATIONS</th>
      <td>-19876.93</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF REVENUE</th>
      <td>-58298.82</td>
    </tr>
    <tr>
      <th>GENERAL SERVICES</th>
      <td>-70981.50</td>
    </tr>
    <tr>
      <th>DEPARTMENT OF ENVIRONMENT</th>
      <td>-76244.10</td>
    </tr>
    <tr>
      <th>OFFICE OF COMPLIANCE</th>
      <td>-81114.55</td>
    </tr>
  </tbody>
</table>
</div>



## Summarize City Financial Data

- per year


```python
fin_years = [2011, 2012, 2013, 2014, 2015, 2016]

# empty lists to append data to
tot_budgets = []
labels = []

# create a dataframe showing the yearly total city budgets from 2011 to 2016
for year in fin_years:
    budget_total = dep_budgets[f"{year} Dept Budgets"].sum()
    tot_budgets.append(budget_total)
    labels.append(f"{year}")
    
# create a dataframe to hold the city financial information    
total_budgets = pd.DataFrame({"Year": labels,
                            "City Budget": tot_budgets})

#Add yearly city financial data to the dataframe
total_budgets["Total Assets"] = yearly_financials["Total Assets"]
total_budgets["Total Liabilities"] = yearly_financials["Total Liabilities"]
total_budgets["Interest Debt"] = yearly_financials["Interest Debt"]
total_budgets["Property Tax Revenue"] = yearly_financials["Property Tax Revenue"]
total_budgets["Total Expenses"] = yearly_financials["Total Expenses"]
total_budgets["Total Revenue"] = yearly_financials["Total Revenue"]
total_budgets["Net Position"] = yearly_financials["Net Position"]

#rearrange dataframe
total_budgets = total_budgets[["Year", "City Budget", "Total Assets", "Total Liabilities", "Interest Debt", "Property Tax Revenue", \
              "Total Expenses", "Total Revenue", "Net Position"]]

# write the dataframe to a csv
total_budgets.to_csv("total_budgets.csv", index=False)

total_budgets[["Year", "City Budget", "Total Assets", "Total Liabilities", "Interest Debt", "Property Tax Revenue", \
              "Total Expenses", "Total Revenue", "Net Position"]]
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
      <th>Year</th>
      <th>City Budget</th>
      <th>Total Assets</th>
      <th>Total Liabilities</th>
      <th>Interest Debt</th>
      <th>Property Tax Revenue</th>
      <th>Total Expenses</th>
      <th>Total Revenue</th>
      <th>Net Position</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2011</td>
      <td>2664496474</td>
      <td>30477700000</td>
      <td>29747300000</td>
      <td>474600000</td>
      <td>934800000</td>
      <td>8582400000</td>
      <td>7543300000</td>
      <td>-2609900000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2012</td>
      <td>2567845412</td>
      <td>30980900000</td>
      <td>31963700000</td>
      <td>459900000</td>
      <td>893300000</td>
      <td>8838600000</td>
      <td>7590800000</td>
      <td>-4283300000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2013</td>
      <td>2609932815</td>
      <td>30744900000</td>
      <td>33395300000</td>
      <td>477900000</td>
      <td>906700000</td>
      <td>8912500000</td>
      <td>7824700000</td>
      <td>-5371100000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2014</td>
      <td>2645370284</td>
      <td>32694700000</td>
      <td>36009500000</td>
      <td>580700000</td>
      <td>926800000</td>
      <td>9319300000</td>
      <td>8154100000</td>
      <td>-6536300000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2015</td>
      <td>2783845781</td>
      <td>42128100000</td>
      <td>62562600000</td>
      <td>861300000</td>
      <td>1179400000</td>
      <td>14364800000</td>
      <td>8947100000</td>
      <td>-23831400000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2016</td>
      <td>2852220338</td>
      <td>41294400000</td>
      <td>64703700000</td>
      <td>495800000</td>
      <td>1264500000</td>
      <td>13003600000</td>
      <td>9405100000</td>
      <td>-27429900000</td>
    </tr>
  </tbody>
</table>
</div>


