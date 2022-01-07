# PyBer_Analysis
## PyBer Analysis Files
#### Cheryl Berger

### Overview of the analysis: Explain the purpose of the new analysis.
The purpose of the analysis was to 
V. Isualize has given you and Omar a brand-new assignment. Using your Python skills and knowledge of Pandas, you’ll create a summary DataFrame of the ride-sharing data by city type. Then, using Pandas and Matplotlib, you’ll create a multiple-line graph that shows the total weekly fares for each city type. Finally, you’ll submit a written report that summarizes how the data differs by city type and how those differences can be used by decision-makers at PyBer.
A ride-sharing summary DataFrame by city type
A multiple-line chart of total fares for each city type

#### Add Matplotlib inline magic command
%matplotlib inline
# Dependencies and Setup
import matplotlib.pyplot as plt
import pandas as pd

#### File to Load (Remember to change these)
city_data_to_load = "Resources\city_data.csv"
ride_data_to_load = "Resources/ride.csv"

##### Read the City and Ride Data
city_data_df = pd.read_csv(city_data_to_load)
ride_data_df = pd.read_csv(ride_data_to_load)

#### Combine the data into a single dataset
pyber_data_df = pd.merge(ride_data_df, city_data_df, how="left", on=["city", "city"])

##### Display the data table for preview
pyber_data_df.head()
![image](https://user-images.githubusercontent.com/94234511/148483493-1f2095ca-eb94-47ef-9647-a21ca3f65700.png)

### Results: Using images from the summary DataFrame and multiple-line chart, describe the differences in ride-sharing data among the different city types.

Using groupby statements get the data to build a summary data frame that includes the following parameters by city type:
Total Rides	Total Drivers	Total Fare	Average Fare per Ride	Average Fare per Driver

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

PyBer_summary_df = pd.DataFrame ({'Total Rides':total_ride_count,
                 'Total Drivers':total_driver_count,
                 'Total Fare':total_fare_count, 
                 'Average Fare per Ride':average_fares_by_type, 
                 'Average Fare per Driver':average_fare_by_driver_count}) 
PyBer_summary_df

![image](https://user-images.githubusercontent.com/94234511/148483966-0c3485b6-9c93-4e70-8d64-5ddb7dcfad09.png)

After removing the index label and formatting the data, the final summary of the ride data by type is displayed below
<Add image of formatted DataFrame>

Next, create a multiple line plot that shows the total weekly of the fares for each type of city.¶

# 1. Read the merged DataFrame
%matplotlib inline

# Dependencies
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

Load the data and merge the DataFrame using the same code described 

 # 2. Using groupby() to create a new DataFrame showing the sum of the fares 
#  for each date where the indices are the city type and date.
total_fare_count_by_type_by_date = pyber_data_df.groupby(["type", "date"]).sum()[["fare"]]
total_fare_count_by_type_by_date 
  
# 3. Reset the index on the DataFrame you created in #1. This is needed to use the 'pivot()' function.
# df = df.reset_index()
total_fare_df = total_fare_count_by_type_by_date.reset_index()
total_fare_df.head()  

# 4. Create a pivot table with the 'date' as the index, the columns ='type', and values='fare' 
# to get the total fares for each type of city by the date. 
total_fare_pivot = total_fare_df.pivot(index="date", columns="type", values="fare")
total_fare_pivot.tail(10)
  
# 5. Create a new DataFrame from the pivot table DataFrame using loc on the given dates, '2019-01-01':'2019-04-29'.
# new_total_fare = total_fare_df.loc[(total_fare_df["date"] == '2019-01-01:2019-04-28')].sum()[["fare"]]
# new_total_fare
# 4. Create a new DataFrame from the pivot table DataFrame using loc on the given dates, '2019-01-01':'2019-04-29'.
fares_Jan_April = total_fare_pivot.loc['2019-01-01':'2019-04-28']
fares_Jan_April.head(20)  
  
# 6. Set the "date" index to datetime datatype. This is necessary to use the resample() method in Step 8.
# df.index = pd.to_datetime(df.index)
fares_Jan_April.index = pd.to_datetime(fares_Jan_April.index)
fares_Jan_April

# 7. Check that the datatype for the index is datetime using df.info()
fares_Jan_April.info()  
  
# 8. Create a new DataFrame using the "resample()" function by week 'W' and get the sum of the fares for each week.
# weekly_total_fare = new_total_fare_df.fare.resample('W').sum()
# weekly_total_fare

weekly_fares_df = fares_Jan_April.resample('W').sum()
weekly_fares_df.head(10)  
![image](https://user-images.githubusercontent.com/94234511/148485146-5a0f8263-408f-43b3-8709-8ca709fe6790.png)

# 8. Using the object-oriented interface method, plot the resample DataFrame using the df.plot() function. 

# Import the style from Matplotlib.
from matplotlib import style
# Use the graph style fivethirtyeight.
style.use('fivethirtyeight')
weekly_fares_df.plot()
plt.ylabel("Fare($USD)")
plt.title("Total Fare by City Type")
# Save the file as PyBer_fare_summary.png
plt.savefig("Resources\PyBer_fare_summary.png")
  http://localhost:8888/view/PyBer%20Challenge/Resources/PyBer_fare_summary.png
   
### Summary: Based on the results, provide three business recommendations to the CEO for addressing any disparities among the city types.
  1) Recommendation 1
  2) Recommendation 2
  3) Recommendation 3
   








