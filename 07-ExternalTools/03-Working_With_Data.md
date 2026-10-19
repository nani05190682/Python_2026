# Working with Data in Python
## Analyze and Visualize Data from APIs

### 1. Building on APIs

In the previous lesson, you learned how to retrieve data from an API using Python. Now, let's turn that raw data into something useful.

We will build a small data analysis project that:

1. Retrieves the past seven days of weather data from an API.
2. Organizes the data using pandas.
3. Calculates average temperatures.
4. Visualizes temperature trends using Matplotlib.
5. Saves the results to CSV and PNG files.

This project combines APIs, Python functions, date handling, data processing, visualization, and file handling.

**Our project workflow:**

```text
Weather API
    |
    v
Retrieve JSON Data
    |
    v
Process with pandas
    |
    v
Analyze Temperatures
    |
    +------> Save CSV File
    |
    +------> Create and Save Chart
```

### 2. Install the required libraries

We will use three Python packages.

| Package | Purpose |
|---|---|
| `requests` | Retrieves data from the weather API. |
| `pandas` | Organizes and analyzes tabular data. |
| `matplotlib` | Creates charts and visualizations. |

Install them inside your project's activated virtual environment:

```bash
python -m pip install requests pandas matplotlib
```

Verify that the packages are installed:

```bash
python -c "import requests, pandas, matplotlib; print('All packages installed successfully')"
```

### 3. Retrieve seven days of weather data

We will use the Open-Meteo Historical Weather API to retrieve daily maximum and minimum temperatures for Paris.

Historical weather data is more appropriate than the forecast endpoint when analyzing previous days. The Historical Weather API provides data for dates that are available in its archive.

Create a file named `weather_analysis.py`.

```python
import requests
from datetime import date, timedelta

# Paris coordinates
latitude = 48.85
longitude = 2.35

# Define the date range
end_date = date.today() - timedelta(days=1)
start_date = end_date - timedelta(days=6)

# API endpoint
url = "https://archive-api.open-meteo.com/v1/archive"

# Query parameters
params = {
    "latitude": latitude,
    "longitude": longitude,
    "start_date": start_date.isoformat(),
    "end_date": end_date.isoformat(),
    "daily": "temperature_2m_max,temperature_2m_min",
    "timezone": "Europe/Paris"
}

# Send the API request
response = requests.get(
    url,
    params=params,
    timeout=20
)

# Check for HTTP errors
response.raise_for_status()

# Convert JSON response to Python data
data = response.json()

# Display the daily weather information
print(data["daily"])
```

Run the program:

```bash
python weather_analysis.py
```

**Understanding the code**

- `date.today()` returns the current date.
- `timedelta(days=1)` represents a one-day interval.
- `timedelta(days=6)` helps define a seven-date range when counting both the start and end dates.
- `isoformat()` converts a date into the `YYYY-MM-DD` format expected by the API.
- `params` specifies the coordinates, date range, daily measurements, and timezone.
- `response.json()` converts the JSON response into Python dictionaries and lists.

We use yesterday as the end date because today's daily observations may be incomplete. If the API does not have data for a requested date, you should handle that possibility in your application.

The API returns daily values similar to these:

```json
{
  "daily": {
    "time": [
      "2026-10-12",
      "2026-10-13",
      "2026-10-14"
    ],
    "temperature_2m_max": [18.5, 20.1, 19.3],
    "temperature_2m_min": [10.2, 11.4, 9.8]
  }
}
```

This is illustrative sample data. Your actual response contains the available dates and measurements for the requested period.

### 4. Load the data into pandas

The API returns structured data, but it is easier to analyze when organized into rows and columns.

Pandas provides a data structure called a **DataFrame**, which works like a table in a spreadsheet or a database query result.

Add the following code after retrieving the API response:

```python
import pandas as pd

daily_data = data["daily"]

df = pd.DataFrame({
    "date": daily_data["time"],
    "max_temp": daily_data["temperature_2m_max"],
    "min_temp": daily_data["temperature_2m_min"]
})

# Convert date strings into datetime values
df["date"] = pd.to_datetime(df["date"])

print(df)
```

Example output:

```text
        date  max_temp  min_temp
0 2026-10-12       18.5      10.2
1 2026-10-13       20.1      11.4
2 2026-10-14       19.3       9.8
```

The displayed values are examples, not actual historical observations.

**What is a DataFrame?**

A DataFrame is a two-dimensional data structure containing rows and columns.

In our example:

- `date` identifies the observation date.
- `max_temp` contains the maximum daily temperature.
- `min_temp` contains the minimum daily temperature.

Converting the date column using `pd.to_datetime()` allows pandas and Matplotlib to work with dates more effectively.

### 5. Analyze the weather data

Now that the data is in a DataFrame, we can calculate useful statistics.

```python
# Calculate the average of daily maximum and minimum temperatures
df["avg_temp"] = (
    df["max_temp"] + df["min_temp"]
) / 2

print("Weather Summary")
print("----------------")

print(f"Average temperature: {df['avg_temp'].mean():.1f}°C")
print(f"Highest maximum temperature: {df['max_temp'].max():.1f}°C")
print(f"Lowest minimum temperature: {df['min_temp'].min():.1f}°C")

print("\nFirst five records:")
print(df.head())
```

**Important distinction:** `avg_temp` here represents the midpoint between each day's maximum and minimum temperatures. It is not necessarily the meteorological daily mean temperature calculated from hourly observations.

Useful pandas operations include:

| Operation | Purpose |
|---|---|
| `df.head()` | Displays the first five rows by default. |
| `df.tail()` | Displays the last five rows by default. |
| `df.shape` | Returns the number of rows and columns. |
| `df.columns` | Lists the column names. |
| `df.mean(numeric_only=True)` | Calculates means for numeric columns. |
| `df.max()` | Finds maximum values. |
| `df.min()` | Finds minimum values. |
| `df.describe()` | Summarizes numeric columns statistically. |

Try:

```python
print(df.shape)
print(df.describe())
```

These operations help you understand the data before creating a chart.

### 6. Visualize the data using Matplotlib

A chart makes temperature trends easier to understand than a table of numbers.

We will create a line chart with three series:

- Daily maximum temperature.
- Daily minimum temperature.
- The midpoint between maximum and minimum temperatures.

```python
import matplotlib.pyplot as plt

plt.figure(figsize=(10, 6))

plt.plot(
    df["date"],
    df["max_temp"],
    marker="o",
    label="Maximum Temperature"
)

plt.plot(
    df["date"],
    df["min_temp"],
    marker="o",
    label="Minimum Temperature"
)

plt.plot(
    df["date"],
    df["avg_temp"],
    linestyle="--",
    label="Midpoint Temperature"
)

plt.xlabel("Date")
plt.ylabel("Temperature (°C)")
plt.title("Paris Weather - Past Seven Days")

plt.legend()
plt.grid(True, alpha=0.3)
plt.xticks(rotation=45)
plt.tight_layout()

plt.show()
```

**Understanding the visualization code**

- `plt.figure(figsize=(10, 6))` creates a figure with a specified size.
- `plt.plot()` draws a line chart.
- `marker="o"` marks each data point.
- `label` defines the series name shown in the legend.
- `plt.xlabel()` and `plt.ylabel()` add axis labels.
- `plt.title()` adds the chart title.
- `plt.legend()` displays the series names.
- `plt.grid()` adds a grid for easier comparison.
- `plt.tight_layout()` adjusts spacing to reduce label overlap.
- `plt.show()` displays the chart.

To save the chart instead of only displaying it, add:

```python
plt.savefig("weather_chart.png", dpi=150, bbox_inches="tight")
```

Call `savefig()` before `show()` so the figure is saved reliably.

### 7. Save the data to a CSV file

A CSV file stores tabular data as rows and columns. It can be opened in spreadsheet software and imported into other analysis tools.

We will create a `data` directory and save the DataFrame.

```python
from pathlib import Path

# Create the output directory if it does not exist
output_dir = Path("data")
output_dir.mkdir(parents=True, exist_ok=True)

# Save the DataFrame
csv_path = output_dir / "paris_weather.csv"

df.to_csv(csv_path, index=False)

print(f"Data saved to {csv_path}")
```

**Why use `index=False`?**

Pandas normally writes the DataFrame's row index to the CSV file. We use `index=False` because our table does not need an additional index column.

**Why use `Path`?**

`pathlib.Path` provides a convenient, cross-platform way to work with file and directory paths.

Your project directory will now contain:

```text
python-data-project/
├── .venv/
├── weather_analysis.py
└── data/
    └── paris_weather.csv
```

The `.venv` directory is created when you set up your virtual environment.

### 8. Complete working example

The following program combines API retrieval, data processing, analysis, visualization, and file saving.

Save it as `weather_analysis.py`.

```python
from datetime import date, timedelta
from pathlib import Path

import matplotlib.pyplot as plt
import pandas as pd
import requests


def fetch_weather(latitude, longitude):
    """Retrieve daily temperatures for the previous seven complete dates."""

    end_date = date.today() - timedelta(days=1)
    start_date = end_date - timedelta(days=6)

    url = "https://archive-api.open-meteo.com/v1/archive"

    params = {
        "latitude": latitude,
        "longitude": longitude,
        "start_date": start_date.isoformat(),
        "end_date": end_date.isoformat(),
        "daily": "temperature_2m_max,temperature_2m_min",
        "timezone": "Europe/Paris"
    }

    response = requests.get(
        url,
        params=params,
        timeout=20
    )

    response.raise_for_status()

    data = response.json()
    daily = data["daily"]

    return pd.DataFrame({
        "date": pd.to_datetime(daily["time"]),
        "max_temp": daily["temperature_2m_max"],
        "min_temp": daily["temperature_2m_min"]
    })


def main():
    # 1. Retrieve weather data for Paris
    df = fetch_weather(48.85, 2.35)

    if df.empty:
        print("No weather data was returned.")
        return

    # 2. Calculate the midpoint between daily maximum and minimum
    df["avg_temp"] = (
        df["max_temp"] + df["min_temp"]
    ) / 2

    # 3. Display the analysis
    print("\nParis Weather Summary")
    print("=====================")
    print(df.to_string(index=False))

    print(
        f"\nAverage midpoint temperature: "
        f"{df['avg_temp'].mean():.1f}°C"
    )

    print(
        f"Highest daily maximum: "
        f"{df['max_temp'].max():.1f}°C"
    )

    print(
        f"Lowest daily minimum: "
        f"{df['min_temp'].min():.1f}°C"
    )

    # 4. Create the output directory
    output_dir = Path("data")
    output_dir.mkdir(parents=True, exist_ok=True)

    # 5. Save the CSV file
    csv_path = output_dir / "paris_weather.csv"
    df.to_csv(csv_path, index=False)

    # 6. Create the chart
    plt.figure(figsize=(10, 6))

    plt.plot(
        df["date"],
        df["max_temp"],
        marker="o",
        label="Maximum"
    )

    plt.plot(
        df["date"],
        df["min_temp"],
        marker="o",
        label="Minimum"
    )

    plt.plot(
        df["date"],
        df["avg_temp"],
        linestyle="--",
        label="Midpoint"
    )

    plt.xlabel("Date")
    plt.ylabel("Temperature (°C)")
    plt.title("Paris Weather - Past Seven Days")
    plt.legend()
    plt.grid(True, alpha=0.3)
    plt.xticks(rotation=45)
    plt.tight_layout()

    # 7. Save the chart
    chart_path = output_dir / "weather_chart.png"
    plt.savefig(chart_path, dpi=150, bbox_inches="tight")
    plt.close()

    print(f"\nCSV saved to: {csv_path}")
    print(f"Chart saved to: {chart_path}")


if __name__ == "__main__":
    try:
        main()
    except requests.exceptions.RequestException as error:
        print(f"Unable to retrieve weather data: {error}")
    except (KeyError, ValueError, TypeError) as error:
        print(f"Unable to process the API response: {error}")
```

Run the program:

```bash
python weather_analysis.py
```

After a successful run, you should have:

```text
data/
├── paris_weather.csv
└── weather_chart.png
```

The CSV contains the processed data, and the PNG contains the chart. The program also prints the weather summary in your terminal.

### 9. Customize the project for your city

You can retrieve weather data for any location supported by the API by changing the latitude and longitude.

For example, approximate coordinates for Bengaluru are:

```python
latitude = 12.97
longitude = 77.59
```

Then update the function call:

```python
df = fetch_weather(12.97, 77.59)
```

If you change the location, also update the timezone and output filenames to match the new city. For Bengaluru, use `Asia/Kolkata` as the timezone.

### 10. Practice exercises

**Exercise 1: Change the location**

Retrieve weather data for Bengaluru instead of Paris.

**Exercise 2: Add another calculation**

Calculate the temperature range for each day:

```python
df["temp_range"] = df["max_temp"] - df["min_temp"]
```

Display the largest daily temperature range.

**Exercise 3: Find the warmest day**

Identify the row with the highest maximum temperature:

```python
warmest_day = df.loc[df["max_temp"].idxmax()]
print(warmest_day)
```

**Exercise 4: Filter the data**

Display only the days when the maximum temperature was greater than 20°C:

```python
warm_days = df[df["max_temp"] > 20]
print(warm_days)
```

**Exercise 5: Improve the chart**

Add a second chart that shows daily temperature ranges.

**Exercise 6: Save a reusable dataset**

Modify the script so that the output CSV filename includes the city name.

### 11. What you have accomplished

You have built a complete data analysis pipeline using Python.

- Retrieved real-world data from an API.
- Worked with dates and time ranges.
- Converted JSON data into a pandas DataFrame.
- Calculated summary statistics.
- Created a line chart using Matplotlib.
- Created directories and saved files.
- Added basic error handling.
- Organized the workflow into reusable functions.

These are foundational skills for data analysis, AI engineering, and automation.

For example, an AI-powered SRE application could use the same approach to retrieve metrics from monitoring APIs, calculate trends, visualize system behavior, and prepare structured data for an AI model.

**Next lesson: Organizing Python Projects — Modules, Packages, and Project Structure.**
