# PyBer_Analysis

#### Cheryl Berger

## Overview of the analysis: Explain the purpose of the new analysis.
The purpose of the analysis is to create a new database of the ride sharing data for PyBer and analyze the weekly fares by city type. V Isualize requested this analysis to assist the CEO in making future business decisions. A report of the analysis will be provide that includes the steps to generate the data summary using Python and a line plot of the fare data generated in Pandas.  The results will be used to compare the differences in ride sharing data by city type.  Finally, a summary of the analysis and recommendations for PyBer to address the disparities in fares by city type.    

The report includes two key outputs: 
1) A ride-sharing summary DataFrame by city type
2) A multiple-line chart of total fares for each city type

### First, create the ride-sharing summary by city type using the Python code below and create a Pandas DataFrames to display the datatable (DataFrame).  

  #### Add Matplotlib inline magic command
  %matplotlib inline
  #### Add Dependencies and Setup packages needed to complete the analysis.  
  import matplotlib.pyplot as plt
  import pandas as pd
  #### Load and read the data files containing the data to be analyzed. 
  city_data_to_load = "Resources\city_d  ata.csv"
  ride_data_to_load = "Resources/ride.csv"
  city_data_df = pd.read_csv(city_data_to_load)
  ride_data_df = pd.read_csv(ride_data_to_load)
  #### Combine the data into a single dataset and display the column headers and first four (4) rows of data for preview
  pyber_data_df = pd.merge(ride_data_df, city_data_df, how="left", on=["city", "city"])
  pyber_data_df.head()
![image](https://user-images.githubusercontent.com/94234511/148483493-1f2095ca-eb94-47ef-9647-a21ca3f65700.png)

## Results: 

### Using the code steps described below, generate the summary data by city type and create the PyBer_Challenge Summary in Pandas DataFrame (see PyBer_Challenge.ipnyb) 

  #### 1) Using groupby statements, get the data to build a summary data frame that includes the following parameters by city type:
                      * Total Rides	
                      * Total Drivers	
                      * Total Fare	
                      * Average Fare per Ride	
                      * Average Fare per Driver

  total_ride_count = pyber_data_df.groupby(["type"]).count()["ride_id"]
  total_ride_count.head()

  total_driver_count = pyber_data_df.groupby(["type"]).sum()["driver_count"]
  total_driver_count.head()

  total_fare_count = pyber_data_df.groupby(["type"]).sum()["fare"]
  total_fare_count.head()

  average_fares_by_type = pyber_data_df.groupby(["type"]).mean()["fare"]
  average_fares_by_type

  average_fare_by_driver_count = pyber_data_df.groupby(["type"]).mean()["driver_count"]
  average_fare_by_driver_count.head()

#### Using Pandas, generate the PyBer_Challenge Summary dataframe and display the table
  PyBer_summary_df = pd.DataFrame ({'Total Rides':total_ride_count,
                   'Total Drivers':total_driver_count,
                   'Total Fare':total_fare_count, 
                   'Average Fare per Ride':average_fares_by_type, 
                   'Average Fare per Driver':average_fare_by_driver_count}) 
  PyBer_summary_df

![image](https://user-images.githubusercontent.com/94234511/148483966-0c3485b6-9c93-4e70-8d64-5ddb7dcfad09.png)

  #### Improve the readability of the DataFrame by removing the index label and formatting the data in each column.  The final summary of the ride data by type is displayed below
  PyBer_summary_df.index.name = None
  PyBer_summary_df = pd.DataFrame ({'Total Rides':total_ride_count,
                 'Total Drivers':total_driver_count,
                 'Total Fare':total_fare_count, 
                 'Average Fare per Ride':average_fares_by_type, 
                 'Average Fare per Driver':average_fare_by_driver_count})

  PyBer_summary_df["Total Rides"] = PyBer_summary_df["Total Rides"].map("{:,}".format)
  PyBer_summary_df["Total Drivers"] = PyBer_summary_df["Total Drivers"].map("{:,}".format)
  PyBer_summary_df["Total Fare"] = PyBer_summary_df["Total Fare"].map("${:,.2f}".format)
  PyBer_summary_df["Average Fare per Ride"] = PyBer_summary_df["Average Fare per Ride"].map("${:,.2f}".format)
  PyBer_summary_df["Average Fare per Driver"] = PyBer_summary_df["Average Fare per Driver"].map("${:,.2f}".format)
  PyBer_summary_df
    
![image](https://user-images.githubusercontent.com/94234511/148553616-db500b20-16f7-4128-9c35-4dc75f8f72fd.png)

  ### The differences in ride-sharing data among the different city types are explained below:
 
  * The total number of rides in the urban cities is the highest with a total of 1625 rides. Urban ride counts are almost triple the number of rides in suburban cities, 625 and about 15 times higher than rural cities, 125 rides. 
  * Similarly, the total number of PyBer drivers varies drastically by city type during the first quarter of 2019.   These data indicate approximately 500 drivers serve the rural cities, 8500 in suburban cities while driver counts near 60,000 in urban cities. This is consistent with earlier reports for these data that indicated the average number of rides in the rural cities was about 3.5 and 2.5 times lower than urban and suburban cities, respectively.
  * The average fare by city type is the highest in the rural cities at $34.62 is the lowest in the urban cities, $24.52
  * The average fare per driver is almost 10 times higher in the urban cities at $36.76 compared to $30.00 and average fares of $4.29 for rural cities.

#### 2) Next, using Pandas and Matplotlib, create a multiple line plot that shows the total weekly of the fares for each type of city.
  #### Read the merged DataFrame
  %matplotlib inline
  #### Import Dependencies
  import matplotlib.pyplot as plt
  import numpy as np
  import pandas as pd
  #### Load the data and merge the DataFrame using the same code described for the summary dataframe then create a new data frame 
  #### Using groupby() to create a new DataFrame showing the sum of the fares for each date where the indices are the city type and date.
  total_fare_count_by_type_by_date = pyber_data_df.groupby(["type", "date"]).sum()[["fare"]]
  total_fare_count_by_type_by_date 
  
  #### Reset the index on the Pandas DataFrame so that the fares for each city type can be parsed by date. Then, create a pivot table with date as the index and display the last   10 rows of the pivot table. 
  total_fare_df = total_fare_count_by_type_by_date.reset_index()
  total_fare_df.head()    
  total_fare_pivot = total_fare_df.pivot(index="date", columns="type", values="fare")
  total_fare_pivot.tail(10)
   
  #### Create a new Pandas DataFrame that covers the ride sharing data from January 1, 2019 through April 29, 2019. 
  fares_Jan_April = total_fare_pivot.loc['2019-01-01':'2019-04-28']
  fares_Jan_April.head(20)  
  #### Set the "date" index to datetime datatype and verify using the df.info() command in Python below 
  fares_Jan_April.index = pd.to_datetime(fares_Jan_April.index)
  fares_Jan_April
  fares_Jan_April.info()   
  #### Finally, create a new DataFrame using the "resample()" function in Python to get the sum of the fares for each week.
  weekly_fares_df = fares_Jan_April.resample('W').sum()
  weekly_fares_df.head(10)  
![image](https://user-images.githubusercontent.com/94234511/148485146-5a0f8263-408f-43b3-8709-8ca709fe6790.png)

#### 3) Using the object-oriented interface method, plot the resample DataFrame
  #### Import the style from Matplotlib.
  from matplotlib import style
  #### Use the graph style fivethirtyeight.
  style.use('fivethirtyeight')
  weekly_fares_df.plot()
  plt.ylabel("Fare($USD)")
  plt.title("Total Fare by City Type")
  #### Save the file as PyBer_fare_summary.png
  plt.savefig("Resources\PyBer_fare_summary.png")
  http://localhost:8888/view/PyBer%20Challenge/Resources/PyBer_fare_summary.png
  ![image](https://user-images.githubusercontent.com/94234511/148487520-952dafb6-86a0-4d02-a124-9b5eec558d00.png)

## Summary: Based on the results, provide three business recommendations to the CEO for addressing any disparities among the city types.
  ### 1) Recommendation 1
  
  ### 2) Recommendation 2
  
  ### 3) Recommendation 3
   








