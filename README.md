# PyBer_Analysis
PyBer Analysis Files
The analysis should contain the following:

Overview of the analysis: Explain the purpose of the new analysis.

# Add Matplotlib inline magic command
%matplotlib inline
# Dependencies and Setup
import matplotlib.pyplot as plt
import pandas as pd

# File to Load (Remember to change these)
city_data_to_load = "Resources\city_data.csv"
ride_data_to_load = "Resources/ride.csv"

# Read the City and Ride Data
city_data_df = pd.read_csv(city_data_to_load)
ride_data_df = pd.read_csv(ride_data_to_load)

# Combine the data into a single dataset
pyber_data_df = pd.merge(ride_data_df, city_data_df, how="left", on=["city", "city"])

# Display the data table for preview
pyber_data_df.head()
![image](https://user-images.githubusercontent.com/94234511/148483493-1f2095ca-eb94-47ef-9647-a21ca3f65700.png)

Results: Using images from the summary DataFrame and multiple-line chart, describe the differences in ride-sharing data among the different city types.

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











Summary: Based on the results, provide three business recommendations to the CEO for addressing any disparities among the city types.

Deliverable 3 Requirements
Structure, Organization, and Formatting (6 points)
The written analysis has the following structure, organization, and formatting:

There is a title, and there are multiple sections. (2 pt)
Each section has a heading and subheading. (2 pt)
Links to images are working and displayed correctly. (2 pt)
Analysis (14 points)
The written analysis has the following:

Overview of the analysis:

The purpose of the new analysis is well defined. (3 pt)
Results:

There is a description of the differences in ride-sharing data among the different city types. Ride-sharing data include the total rides, total drivers, total fares, average fare per ride and driver, and total fare by city type. (7 pt)
Summary:

There is a statement summarizing three business recommendations to the CEO for addressing any disparities among the city types. (4 pt)
