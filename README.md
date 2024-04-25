Q2 Data Cleaning: 1) Merge the cost schedule for different parking systems into the cars_per_parking_sys.csv dataset. 2) After merging, create a column indicating the price paid by vehicles for each parking system at the time they switch to a zero-cost fare, based on the provided information about the timing of the switch.

Q3 Data Exploration: Analyze how the transition to free parking impacts parking activity.

Q4 Estimation: Estimate the effect of parking cost on the number of parked vehicles.

Q5 Big Data Processing: Assuming the computer can only handle 200K rows of data in RAM at once, the database containing data from parking systems psres_33, psres_34, psres_35, and psres_36 is corrupted. The raw data dump is available in raw_park_sys_info_df.csv. Note that this data dump represents the unprocessed data used to generate the data found in cars_per_parking_sys.csv. 
- Based on patterns in the number of cars parked for these 4 parking systems, identify which of the parking systems, if any, have errors in data logging. (Note: the one-off missing values handled in the data cleaning step shouldn’t be a concern here)
- One possible reason for problematic patterns seen in the erroneous parking systems could be due to mislogging of vehicles
  - When vehicles fail to get registered in a timestamp but the system handles the error gracefully, you will see a “-99” in the “vehicle_ids” columns for that timestamp in the raw data. “num_vehicles” for this parking system- timestamp combination in cars_per_parking_sys.csv is then handled as a missing value. Such cases are not considered very problematic.
  - More problematic are cases when vehicles get registered in the wrong timestamp.
  - In such cases, the timestamp where vehicles failed to get registered will have the string “LogError” in the “vehicle_ids” column.
  - These vehicles then get registered in a subsequent timestamp. Vehicles that are misregistered like this will be registered with a vehicle ID that’s shorter than 16 characters in length.
  - To correct these cases, please replace the “LogErrors” with “-99”, remove cases where vehicle IDs are shorter than 16 characters in length, and regenerate the equivalent of cars_per_parking_sys.csv for the parking system(s) that have this issue.
  - To output the summary statistics of this corrected dataset, and recreate the trend figures you created to diagnose the issue in 5.1.

You can download the complete coding sample folder, including the coding file and the mentioned datasets,(Please download the entire coding_sample_folder to run the code successfully): 
https://www.dropbox.com/scl/fo/4hzdoeetvnzw9sainpvdt/APu01qUYf8BJPwNvQUtRwj8?rlkey=6cnweh192ghpo84a844agidu0&dl=0
