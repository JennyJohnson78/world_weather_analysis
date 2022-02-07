# World Weather Analysis

## Overview
APIs, or an Application Programming Interface, is a software intermediary that allows two applications to talk to each other. This technology is used extensively in software and web development, as well as data analytics and data science. APIs can be used to retrieve data from the web. Using the Google Maps Directions API, weather data will be filtered by preferences, which will be used to identify potential travel destinations and nearby hotels. Within this analysis, a travel route between the four cities will be created, as well as a marker layer map.

## Results

### API Call

- First, an API call is made to gather weather data using the URL below
```
# Starting URL for Weather Map API Call.
url = "http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=92eb438c0120869d3296ae56bfb217e4"
```

- Next, the weather data is added to a DataFrame

```
# Convert the array of dictionaries to a Pandas DataFrame.
city_data_df = pd.DataFrame(city_data)
city_data_df.head(10)
```

- Then, this data is exported as a CSV file
```
# Create the output file (CSV).
output_data_file = "WeatherPy_Database.csv"
# Export the City_Data into a CSV.
city_data_df.to_csv(output_data_file, index_label="City_ID")
```

![image](https://user-images.githubusercontent.com/67409852/139557648-a66628f2-4484-4748-b027-1e6a19b6b876.png)

### Create Markup Layer Map

- Write two input statements that prompt the user to enter their minimum and maximum temperature criteria for their vacation

```
# Prompt the user to enter minimum and maximum temperature criteria 
min_temp = float(input("What is the minimun temperature you would like for your trip? "))
max_temp = float(input("What is the maximun temperature you would like for your trip? "))
```

- Next, use the loc method to to filter the DataFrame for that temperature criteria

```
# Filter the city_data_df DataFrame using the input statements to create a new DataFrame using the loc method.
preferred_cities_df = city_data_df.loc[(city_data_df["Max Temp"] >= min_temp) & (city_data_df["Max Temp"] <= max_temp)]
preferred_cities_df.head()
```

- Iterate through the hotels DataFrame using a for loop and retrieve their latitude and longitude and add this to a new DataFrame

- Then, add the city name, the country code, the weather description, and the maximum temperature for the city

```
# Using the template add city name, the country code, the weather description and maximum temperature for the city.
info_box_template = """
<dl>
<dt>Hotel Name</dt><dd>{Hotel Name}</dd>
<dt>City</dt><dd>{City}</dd>
<dt>Country</dt><dd>{Country}</dd>
<dt>Weather Description</dt>
<dt>Max Temp</dt><dd>{Max Temp} °F</dd>
</dl>
"""
```

- Refactor the previous marker layer map code to create a marker layer map that will have pop-up markers for each city on the map

```
# Add a marker layer for each city to the map. 
fig = gmaps.figure(center=(30.0, 31.0), zoom_level=1.5)
markers = gmaps.marker_layer(locations, info_box_content=hotel_info)
fig.add_layer(markers)
```

![image](https://user-images.githubusercontent.com/67409852/139627528-fb7cfb8d-fea1-40c0-bf3c-e11ca8e8ad75.png)


![image](https://user-images.githubusercontent.com/67409852/139613419-9245e88e-5172-4457-9991-22b2610b6f7d.png)
