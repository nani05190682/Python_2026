# Working with APIs in Python
## Pull Data from Web Services

### 1. What is an API?

An **API (Application Programming Interface)** allows one software application to communicate with another application or service.

Imagine you are at a restaurant. You tell the waiter what you want, the waiter communicates your request to the kitchen, and then brings your food back.

An API works in a similar way:

- **Your Python program:** Makes a request.
- **API:** Receives and processes the request.
- **Server:** Finds or processes the requested information.
- **Response:** Returns the result to your Python program.

APIs do more than retrieve information. They also allow applications to create records, update information, and trigger actions.

**Real-world examples:**

- Retrieve customer information from Salesforce or HubSpot.
- Get order details from Shopify or WooCommerce.
- Send messages using Slack APIs.
- Retrieve weather forecasts from a weather API.
- Send prompts to AI models through AI provider APIs.
- Collect server metrics and incident information for an AI-powered SRE agent.

In AI engineering, APIs are especially important because they connect AI models to business data, applications, and infrastructure.

### 2. How does an API request work?

A typical API interaction follows this sequence:

1. Your Python program sends an HTTP request.
2. The API server processes the request.
3. The server returns an HTTP response.
4. Python reads the response, often in JSON format.
5. Your program extracts and uses the required data.

For example:

```text
Python Program
      |
      | HTTP GET Request
      v
Weather API
      |
      | JSON Response
      v
Python Program
      |
      v
Display Temperature
```

### 3. Prepare your Python environment

We will use the `requests` package to communicate with a web API.

First, create and activate a virtual environment if you do not already have one.

**Windows PowerShell**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install requests
```

**Linux or macOS**

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install requests
```

You can verify the installation:

```bash
python -c "import requests; print(requests.__version__)"
```

The `requests` package makes HTTP requests easier to write and understand.

### 4. Make your first API call

Let's retrieve the current weather for Paris using the free [Open-Meteo API](https://open-meteo.com/).

Create a file named `weather_api.py`.

```python
import requests

# Coordinates for Paris
latitude = 48.85
longitude = 2.35

# API endpoint
url = "https://api.open-meteo.com/v1/forecast"

# Parameters to send to the API
params = {
    "latitude": latitude,
    "longitude": longitude,
    "current": "temperature_2m"
}

# Send an HTTP GET request
response = requests.get(
    url,
    params=params,
    timeout=10
)

# Check whether the request was successful
response.raise_for_status()

# Convert the JSON response into Python data
data = response.json()

# Display the response
print(data)
```

Run the program:

```bash
python weather_api.py
```

The response contains weather information and metadata. The exact values depend on the API response at the time you run the program.

**What does each part do?**

| Code | Purpose |
|---|---|
| `import requests` | Imports the HTTP client package. |
| `url` | Specifies the API endpoint. |
| `params` | Contains the query parameters. |
| `requests.get()` | Sends an HTTP GET request. |
| `timeout=10` | Limits how long the client waits for a response. |
| `raise_for_status()` | Raises an exception for unsuccessful HTTP status codes. |
| `response.json()` | Parses the JSON response into Python objects. |

Using `params` is preferable to manually building a long URL because `requests` handles URL encoding for you.

### 5. Understand the API response

Many APIs return data in **JSON (JavaScript Object Notation)** format.

JSON is a text-based format for exchanging structured data between applications. It supports objects, arrays, strings, numbers, booleans, and `null`.

For example, an API might return this JSON:

```json
{
  "latitude": 48.85,
  "longitude": 2.35,
  "timezone": "Europe/Paris",
  "current_units": {
    "temperature_2m": "°C"
  },
  "current": {
    "time": "2026-10-19T08:00",
    "temperature_2m": 18.5
  }
}
```

*This is an illustrative example; your actual response will differ.*

After calling `response.json()`, Python converts the JSON object into a dictionary. Nested JSON objects become nested dictionaries.

You can retrieve the temperature like this:

```python
temperature = data["current"]["temperature_2m"]

print(f"Temperature in Paris: {temperature}°C")
```

Example output:

```text
Temperature in Paris: 18.5°C
```

The output is illustrative, not a live weather reading.

**Understanding nested dictionaries**

```python
data["current"]["temperature_2m"]
```

Python performs two lookups:

1. `data["current"]` retrieves the nested dictionary containing current weather.
2. `["temperature_2m"]` retrieves the temperature from that dictionary.

Remember that dictionary keys are case-sensitive. Use the exact keys returned by the API.

### 6. Extract only the information you need

Let's improve our code by creating a reusable function. This function will retrieve the temperature and wind speed for any coordinates.

```python
import requests

def get_weather(latitude, longitude):
    url = "https://api.open-meteo.com/v1/forecast"

    params = {
        "latitude": latitude,
        "longitude": longitude,
        "current": "temperature_2m,wind_speed_10m"
    }

    response = requests.get(
        url,
        params=params,
        timeout=10
    )

    response.raise_for_status()

    data = response.json()
    current_weather = data["current"]

    return {
        "temperature": current_weather["temperature_2m"],
        "wind_speed": current_weather["wind_speed_10m"]
    }


# Coordinates for three cities
cities = {
    "Paris": (48.85, 2.35),
    "London": (51.50, -0.12),
    "Tokyo": (35.68, 139.69)
}

for city, coordinates in cities.items():
    latitude, longitude = coordinates

    weather = get_weather(latitude, longitude)

    print(
        f"{city}: "
        f"{weather['temperature']}°C, "
        f"Wind: {weather['wind_speed']} km/h"
    )
```

Example output:

```text
Paris: 18.5°C, Wind: 12.3 km/h
London: 15.2°C, Wind: 9.8 km/h
Tokyo: 22.1°C, Wind: 7.4 km/h
```

The output above is illustrative. Actual values vary with current weather.

**What have we learned?**

- We created a function to avoid repeating API logic.
- We passed different coordinates as function arguments.
- We extracted only the fields we needed.
- We returned the extracted data as a dictionary.
- We used a `for` loop to process multiple cities.

This pattern is useful whenever you need to retrieve data from multiple services or process many API responses.

### 7. Understand HTTP status codes

An API request can succeed or fail. HTTP status codes help you understand the result.

| Status code | Meaning |
|---|---|
| `200 OK` | The request succeeded. |
| `201 Created` | A resource was created successfully. |
| `400 Bad Request` | The request contains invalid input. |
| `401 Unauthorized` | Authentication is missing or invalid. |
| `403 Forbidden` | Access is not permitted. |
| `404 Not Found` | The requested resource was not found. |
| `429 Too Many Requests` | The API rate limit was exceeded. |
| `500 Internal Server Error` | The server encountered an error. |
| `503 Service Unavailable` | The service is temporarily unavailable. |

You can inspect the status code directly:

```python
print(response.status_code)
```

For successful requests, you might see:

```text
200
```

You should not assume that every HTTP response is successful. Using `raise_for_status()` helps prevent your program from silently processing an error response as if it were valid data.

### 8. Handle API errors safely

Network requests can fail because of connectivity problems, timeouts, invalid responses, or server errors.

Let's add basic error handling.

```python
import requests

def get_temperature(latitude, longitude):
    url = "https://api.open-meteo.com/v1/forecast"

    params = {
        "latitude": latitude,
        "longitude": longitude,
        "current": "temperature_2m"
    }

    try:
        response = requests.get(
            url,
            params=params,
            timeout=10
        )

        response.raise_for_status()

        data = response.json()
        return data["current"]["temperature_2m"]

    except requests.exceptions.Timeout:
        print("The API request timed out.")

    except requests.exceptions.HTTPError as error:
        print(f"HTTP error: {error}")

    except requests.exceptions.RequestException as error:
        print(f"Network error: {error}")

    except (ValueError, KeyError, TypeError):
        print("The API response was not in the expected format.")

    return None


temperature = get_temperature(48.85, 2.35)

if temperature is not None:
    print(f"Temperature: {temperature}°C")
else:
    print("Unable to retrieve the temperature.")
```

This example separates common network and response errors from normal processing.

In a production application, you would typically log errors instead of relying only on `print()`. You may also need retry logic, rate-limit handling, and validation of the returned data.

### 9. What are query parameters?

Query parameters are values sent to an API to control what information it returns.

For example:

```text
https://api.example.com/weather?city=Paris&units=metric
```

Here:

- `city=Paris` specifies the city.
- `units=metric` requests metric measurements.
- `&` separates the parameters.

In Python, use a dictionary:

```python
params = {
    "city": "Paris",
    "units": "metric"
}

response = requests.get(
    "https://api.example.com/weather",
    params=params,
    timeout=10
)
```

The example endpoint above is illustrative and is not a real service. The earlier Open-Meteo example demonstrates a working public API pattern.

### 10. How APIs are used in AI engineering

APIs are a fundamental building block of AI applications.

| Use case | Example |
|---|---|
| AI assistants | Send a prompt to an AI model API. |
| Retrieval-augmented generation (RAG) | Retrieve documents or records from a search service. |
| Business automation | Retrieve customer or order data. |
| AI-powered SRE | Query monitoring and log-management APIs. |
| Cloud automation | Retrieve infrastructure information from cloud APIs. |
| Incident analysis | Collect alerts, logs, and metrics before asking an AI model to summarize them. |

For example, an AI-powered SRE agent could follow this workflow:

1. Query Prometheus for CPU and memory metrics.
2. Retrieve relevant logs from Elasticsearch.
3. Identify the affected host or service.
4. Send the collected evidence to an AI model for analysis.
5. Produce a diagnosis and recommended remediation.
6. Request human approval before executing any potentially disruptive action.

This approach combines APIs, Python functions, structured data, and AI reasoning.

### 11. API security best practices

When working with real APIs:

- **Protect API keys:** Store secrets in environment variables or a secrets manager, not directly in source code.
- **Use HTTPS:** Protect data while it travels between your application and the service.
- **Set timeouts:** Avoid waiting indefinitely for a response.
- **Handle errors:** Account for timeouts, rate limits, and unsuccessful HTTP status codes.
- **Validate responses:** Do not blindly trust external data.
- **Follow rate limits:** Avoid sending excessive requests.
- **Use least privilege:** Give API credentials only the permissions they require.
- **Avoid logging secrets:** Never print access tokens, passwords, or API keys in logs.

### 12. Practice exercises

**Exercise 1: Retrieve weather**

Modify the first example to retrieve the current temperature for Bengaluru.

Hint: Bengaluru is approximately latitude `12.97`, longitude `77.59`.

**Exercise 2: Extract multiple fields**

Retrieve both the temperature and wind speed. Print them in a readable format.

**Exercise 3: Create a reusable function**

Write a function named `get_weather(latitude, longitude)` that returns the temperature.

**Exercise 4: Handle failures**

Add a `try`/`except` block so your program handles network errors gracefully.

**Exercise 5: Process multiple cities**

Retrieve weather data for Bengaluru, Chennai, and Mumbai using a dictionary and a `for` loop.

### 13. Sample solution: Bengaluru weather

```python
import requests

def get_weather(latitude, longitude):
    url = "https://api.open-meteo.com/v1/forecast"

    params = {
        "latitude": latitude,
        "longitude": longitude,
        "current": "temperature_2m,wind_speed_10m"
    }

    try:
        response = requests.get(
            url,
            params=params,
            timeout=10
        )

        response.raise_for_status()

        data = response.json()
        current = data["current"]

        return {
            "temperature": current["temperature_2m"],
            "wind_speed": current["wind_speed_10m"]
        }

    except (
        requests.exceptions.RequestException,
        ValueError,
        KeyError,
        TypeError
    ) as error:
        print(f"Unable to retrieve weather: {error}")
        return None


weather = get_weather(12.97, 77.59)

if weather is not None:
    print(f"Bengaluru temperature: {weather['temperature']}°C")
    print(f"Wind speed: {weather['wind_speed']} km/h")
```

This example combines functions, dictionaries, HTTP requests, JSON parsing, and exception handling.

### 14. Lesson summary

In this lesson, you learned:

- What an API is and how applications communicate.
- How to install and use the `requests` package.
- How to send HTTP GET requests.
- How to pass query parameters.
- How to parse JSON into Python dictionaries.
- How to extract nested data.
- How to create reusable API functions.
- How to inspect HTTP status codes and handle errors.
- How APIs support AI engineering, cloud automation, and SRE workflows.

**Key takeaway:** An API allows your Python program to interact with external services. The essential pattern is to send a request, check the response, parse the returned data, and use the information in your application.

**Next lesson: Working with JSON — Read, Create, and Transform Structured Data.**
