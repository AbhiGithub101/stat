---
hidden: true
---

# Weather Data Analyzer

> **Level:** Beginner–Intermediate\
> **Topics Used:** Data Types, Variables, Operators, Typecasting, Strings, Functions, Conditionals, Loops, List, Set, Tuple, Dictionary, User Input, File Handling\
> **API Used:** [WeatherAPI.com](https://www.weatherapi.com/) _(Free Plan)_

***

## &#x20;What Will You Build?

A Python program that:

* Asks the user to enter a **city name**
* Fetches **live weather data** from the internet using an API
* Shows **current weather** + **3-day forecast**
* Gives **weather alerts** based on temperature
* Lets user **filter data** by condition (Sunny, Rainy, etc.)
* **Saves a report** to a `.txt` file and raw data to `.json`

***

## &#x20;What is an API?

**API = Application Programming Interface**

Think of it like a **waiter in a restaurant**:

* You (your Python code) = Customer
* API = Waiter
* Weather Server = Kitchen

You give an order (request) → Waiter goes to the kitchen → Brings back food (data).

**In simple terms,** an API gives you data from another website/server, without you visiting it manually.

***

## Step 0: Get Your Free API Key

1. Go to [https://www.weatherapi.com](https://www.weatherapi.com/)
2. Click **Sign Up** → Create a free account
3. After login, your **API Key** will be visible on the dashboard
4. Copy it - you'll paste it in your code

> ⚠️ **Never share your API Key publicly.** It's like a password.

***

## &#x20;Project Structure

```
weather_project/
├── analyzer.py          ← Main Python file (you will write this)
├── weather_data.json    ← Auto-created when you run the program
└── report.txt           ← Auto-created report
```

***

## &#x20;No Extra Libraries Needed

We use Python's built-in `urllib.request` and `json` - **No pip install required**.

```python
import json
import urllib.request
```

***

## &#x20; Full Code - Step by Step

{% stepper %}
{% step %}
### Configuration (Variables)

```python
API_KEY = "YOUR_API_KEY"   # Paste your key here
```

**Topic:** Variables, Strings\
**Why:** We store the API key in a variable so we can reuse it easily.
{% endstep %}

{% step %}
### Get City from User (User Input)

```python
def get_city():
    city = input(" Enter city name: ").strip()
    if not city:
        print("City name cannot be blank!")
        return get_city()   # Ask again if blank
    return city
```

**Topic:** User Input, String methods (`.strip()`), Functions, Conditionals\
**Real-world use:** Every weather app asks you to type a city - this is how it works.
{% endstep %}

{% step %}
### Fetch Data from API (API Call)

```python
def fetch_weather(city):
    current_url = f"http://api.weatherapi.com/v1/current.json?key={API_KEY}&q={city}&aqi=no"
    forecast_url = f"http://api.weatherapi.com/v1/forecast.json?key={API_KEY}&q={city}&days=3&aqi=no"

    print("\n📡 Fetching data from API...")

    try:
        with urllib.request.urlopen(current_url) as response:
            current_data = json.loads(response.read().decode())

        with urllib.request.urlopen(forecast_url) as response:
            forecast_data = json.loads(response.read().decode())

        print(" Data fetched successfully!\n")
        return current_data, forecast_data

    except Exception as e:
        print(f"❌ Error: {e}")
        return None, None
```

**Topic:** Functions, Strings (f-string), Dictionary (API returns JSON = dict)\
**What is JSON?** JSON is just a **dictionary format** that APIs use to send data. Python reads it as a `dict`.

> &#x20; **URL Breakdown:**
>
> * `http://api.weatherapi.com/v1/current.json` → API address
> * `?key=YOUR_KEY` → Your identity
> * `&q=Kanpur` → Your query (city name)
> * `&aqi=no` → We don't need air quality data
{% endstep %}

{% step %}
### Save Raw Data to JSON File (File Handling)

```python
def save_raw_data(current_data, forecast_data):
    combined = {
        "current": current_data,
        "forecast": forecast_data
    }
    with open("weather_data.json", "w") as f:
        json.dump(combined, f, indent=4)
    print("💾 Raw data saved → weather_data.json")
```

**Topic:** File Handling, Dictionary\
**Real-world use:** Data Analysts always save raw data first before analyzing. This is called **data storage**.
{% endstep %}

{% step %}
### Show Current Weather (Variables + Typecasting + Strings)

```python
def show_current_weather(data):
    loc = data["location"]
    cur = data["current"]

    city_name  = loc["name"]               # String
    country    = loc["country"]            # String
    temp_c     = float(cur["temp_c"])      # Typecasting: str → float
    feels_like = float(cur["feelslike_c"])
    humidity   = int(cur["humidity"])      # Typecasting: str → int
    wind_kph   = float(cur["wind_kph"])
    condition  = cur["condition"]["text"]
    uv_index   = cur["uv"]

    print("=" * 40)
    print(f"📍 {city_name.upper()}, {country}")
    print("=" * 40)
    print(f"🌡️  Temperature  : {temp_c}°C  (Feels like {feels_like}°C)")
    print(f"💧 Humidity     : {humidity}%")
    print(f"💨 Wind Speed   : {wind_kph} kph")
    print(f"☁️  Condition    : {condition}")
    print(f"☀️  UV Index     : {uv_index}")

    # Conditional Alerts
    if uv_index >= 8:
        print("⚠️  UV Alert: Apply sunscreen!")
    if humidity >= 70:
        print("⚠️  Humidity Alert: Very humid today!")
    if wind_kph >= 40:
        print("⚠️  Wind Alert: Strong winds!")

    return temp_c, humidity, condition
```

**Topic:** Variables, Typecasting, String (f-string, `.upper()`), Conditionals, Dictionary access\
**Why Typecasting?** API sends some values as strings — we convert them to `float`/`int` for math operations.
{% endstep %}

{% step %}
### Show 3-Day Forecast (List + Set + Loop + Dictionary)

```python
def show_forecast(forecast_data):
    days = forecast_data["forecast"]["forecastday"]   # List of dicts

    print("\n📅 3-Day Forecast:")
    print("-" * 40)

    temps = []           # List — collect all max temps
    conditions = set()   # Set — unique conditions only

    for day in days:     # Loop through each day
        date      = day["date"]
        max_temp  = float(day["day"]["maxtemp_c"])
        min_temp  = float(day["day"]["mintemp_c"])
        avg_temp  = float(day["day"]["avgtemp_c"])
        condition = day["day"]["condition"]["text"]
        rain_pct  = day["day"]["daily_chance_of_rain"]

        temps.append(max_temp)       # Add to list
        conditions.add(condition)    # Add to set (auto-removes duplicates)

        # Alert logic
        if max_temp >= 40:
            alert = "🔴 Heat Wave"
        elif max_temp >= 35:
            alert = "🟡 Hot Day"
        elif rain_pct >= 70:
            alert = "🌧️  High Rain Chance"
        else:
            alert = "✅ Normal"

        print(f"\n  📆 {date}")
        print(f"     Max: {max_temp}°C | Min: {min_temp}°C | Avg: {avg_temp}°C")
        print(f"     Condition: {condition} | Rain Chance: {rain_pct}%")
        print(f"     Alert: {alert}")

    return temps, conditions
```

**Topic:** List, Set, Loop, Dictionary, Conditionals, Typecasting\
**Why Set?** If all 3 days are "Sunny", set stores it only once - no duplicates.
{% endstep %}

{% step %}
### Calculate Stats (Operators + Tuple)

```python
def show_stats(temps, conditions):
    avg = round(sum(temps) / len(temps), 2)       # Operators
    temp_range = (min(temps), max(temps))          # Tuple

    print("\n📊 Forecast Summary:")
    print(f"   Avg Max Temp : {avg}°C")
    print(f"   Temp Range   : {temp_range[0]}°C – {temp_range[1]}°C")
    print(f"   Conditions   : {conditions}")

    return avg, temp_range
```

**Topic:** Operators (`/`, `sum`, `round`), Tuple\
**Why Tuple?** `temp_range` stores `(min, max)` - two values that belong together and shouldn't change.
{% endstep %}

{% step %}
### Filter by Condition (User Input + Loop + Conditionals)

```python
def filter_by_condition(forecast_data):
    user_input = input("\n🔍 Filter days by condition (Sunny / Rainy / Cloudy): ").strip().lower()

    days = forecast_data["forecast"]["forecastday"]
    print(f"\n📋 Days with '{user_input.capitalize()}' condition:")

    found = False
    for day in days:
        condition = day["day"]["condition"]["text"].lower()
        if user_input in condition:
            print(f"  {day['date']} → {day['day']['maxtemp_c']}°C | {day['day']['condition']['text']}")
            found = True

    if not found:
        print("  No matching days found.")
```

**Topic:** User Input, String methods (`.lower()`, `.capitalize()`, `.strip()`), Loop, Conditionals
{% endstep %}

{% step %}
### Save Report to .txt File (File Handling)

```python
def save_report(city, current_data, avg, temp_range, conditions):
    cur = current_data["current"]

    with open("report.txt", "w") as f:
        f.write(f"Weather Report — {city.upper()}\n")
        f.write("=" * 40 + "\n\n")
        f.write("[Current Weather]\n")
        f.write(f"Temperature  : {cur['temp_c']}°C\n")
        f.write(f"Feels Like   : {cur['feelslike_c']}°C\n")
        f.write(f"Humidity     : {cur['humidity']}%\n")
        f.write(f"Wind Speed   : {cur['wind_kph']} kph\n")
        f.write(f"Condition    : {cur['condition']['text']}\n\n")
        f.write("[3-Day Forecast Stats]\n")
        f.write(f"Avg Max Temp : {avg}°C\n")
        f.write(f"Temp Range   : {temp_range[0]}°C – {temp_range[1]}°C\n")
        f.write(f"Conditions   : {', '.join(conditions)}\n")

    print("\n✅ Report saved → report.txt")
```

**Topic:** File Handling (`open`, `write`), String formatting\
**Real-world use:** Analysts generate automated reports - this is your first automated report!
{% endstep %}

{% step %}
### Main Function (Putting It All Together)

```python
def main():
    city = get_city()
    current_data, forecast_data = fetch_weather(city)

    if not current_data or not forecast_data:
        print("Could not fetch data. Exiting.")
        return

    save_raw_data(current_data, forecast_data)
    temp_c, humidity, condition = show_current_weather(current_data)
    temps, conditions = show_forecast(forecast_data)
    avg, temp_range = show_stats(temps, conditions)
    filter_by_condition(forecast_data)
    save_report(city, current_data, avg, temp_range, conditions)

main()
```
{% endstep %}
{% endstepper %}

***

## &#x20;Complete Code&#x20;

```python
import json
import urllib.request

API_KEY = "YOUR_API_KEY"

def get_city():
    city = input("🌍 Enter city name: ").strip()
    if not city:
        print("City name cannot be blank!")
        return get_city()
    return city

def fetch_weather(city):
    current_url = f"http://api.weatherapi.com/v1/current.json?key={API_KEY}&q={city}&aqi=no"
    forecast_url = f"http://api.weatherapi.com/v1/forecast.json?key={API_KEY}&q={city}&days=3&aqi=no"
    print("\n📡 Fetching data from API...")
    try:
        with urllib.request.urlopen(current_url) as response:
            current_data = json.loads(response.read().decode())
        with urllib.request.urlopen(forecast_url) as response:
            forecast_data = json.loads(response.read().decode())
        print("✅ Data fetched successfully!\n")
        return current_data, forecast_data
    except Exception as e:
        print(f"❌ Error: {e}")
        return None, None

def save_raw_data(current_data, forecast_data):
    combined = {"current": current_data, "forecast": forecast_data}
    with open("weather_data.json", "w") as f:
        json.dump(combined, f, indent=4)
    print("💾 Raw data saved → weather_data.json")

def show_current_weather(data):
    loc = data["location"]
    cur = data["current"]
    city_name  = loc["name"]
    country    = loc["country"]
    temp_c     = float(cur["temp_c"])
    feels_like = float(cur["feelslike_c"])
    humidity   = int(cur["humidity"])
    wind_kph   = float(cur["wind_kph"])
    condition  = cur["condition"]["text"]
    uv_index   = cur["uv"]
    print("=" * 40)
    print(f"📍 {city_name.upper()}, {country}")
    print("=" * 40)
    print(f"🌡️  Temperature  : {temp_c}°C  (Feels like {feels_like}°C)")
    print(f"💧 Humidity     : {humidity}%")
    print(f"💨 Wind Speed   : {wind_kph} kph")
    print(f"☁️  Condition    : {condition}")
    print(f"☀️  UV Index     : {uv_index}")
    if uv_index >= 8:
        print("⚠️  UV Alert: Apply sunscreen!")
    if humidity >= 70:
        print("⚠️  Humidity Alert: Very humid today!")
    if wind_kph >= 40:
        print("⚠️  Wind Alert: Strong winds!")
    return temp_c, humidity, condition

def show_forecast(forecast_data):
    days = forecast_data["forecast"]["forecastday"]
    print("\n📅 3-Day Forecast:")
    print("-" * 40)
    temps = []
    conditions = set()
    for day in days:
        date      = day["date"]
        max_temp  = float(day["day"]["maxtemp_c"])
        min_temp  = float(day["day"]["mintemp_c"])
        avg_temp  = float(day["day"]["avgtemp_c"])
        condition = day["day"]["condition"]["text"]
        rain_pct  = day["day"]["daily_chance_of_rain"]
        temps.append(max_temp)
        conditions.add(condition)
        if max_temp >= 40:
            alert = "🔴 Heat Wave"
        elif max_temp >= 35:
            alert = "🟡 Hot Day"
        elif rain_pct >= 70:
            alert = "🌧️  High Rain Chance"
        else:
            alert = "✅ Normal"
        print(f"\n  📆 {date}")
        print(f"     Max: {max_temp}°C | Min: {min_temp}°C | Avg: {avg_temp}°C")
        print(f"     Condition: {condition} | Rain Chance: {rain_pct}%")
        print(f"     Alert: {alert}")
    return temps, conditions

def show_stats(temps, conditions):
    avg = round(sum(temps) / len(temps), 2)
    temp_range = (min(temps), max(temps))
    print("\n📊 Forecast Summary:")
    print(f"   Avg Max Temp : {avg}°C")
    print(f"   Temp Range   : {temp_range[0]}°C – {temp_range[1]}°C")
    print(f"   Conditions   : {conditions}")
    return avg, temp_range

def filter_by_condition(forecast_data):
    user_input = input("\n🔍 Filter days by condition (Sunny / Rainy / Cloudy): ").strip().lower()
    days = forecast_data["forecast"]["forecastday"]
    print(f"\n📋 Days with '{user_input.capitalize()}' condition:")
    found = False
    for day in days:
        condition = day["day"]["condition"]["text"].lower()
        if user_input in condition:
            print(f"  {day['date']} → {day['day']['maxtemp_c']}°C | {day['day']['condition']['text']}")
            found = True
    if not found:
        print("  No matching days found.")

def save_report(city, current_data, avg, temp_range, conditions):
    cur = current_data["current"]
    with open("report.txt", "w") as f:
        f.write(f"Weather Report — {city.upper()}\n")
        f.write("=" * 40 + "\n\n")
        f.write("[Current Weather]\n")
        f.write(f"Temperature  : {cur['temp_c']}°C\n")
        f.write(f"Feels Like   : {cur['feelslike_c']}°C\n")
        f.write(f"Humidity     : {cur['humidity']}%\n")
        f.write(f"Wind Speed   : {cur['wind_kph']} kph\n")
        f.write(f"Condition    : {cur['condition']['text']}\n\n")
        f.write("[3-Day Forecast Stats]\n")
        f.write(f"Avg Max Temp : {avg}°C\n")
        f.write(f"Temp Range   : {temp_range[0]}°C – {temp_range[1]}°C\n")
        f.write(f"Conditions   : {', '.join(conditions)}\n")
    print("\n✅ Report saved → report.txt")

def main():
    city = get_city()
    current_data, forecast_data = fetch_weather(city)
    if not current_data or not forecast_data:
        print("Could not fetch data. Exiting.")
        return
    save_raw_data(current_data, forecast_data)
    temp_c, humidity, condition = show_current_weather(current_data)
    temps, conditions = show_forecast(forecast_data)
    avg, temp_range = show_stats(temps, conditions)
    filter_by_condition(forecast_data)
    save_report(city, current_data, avg, temp_range, conditions)

main()
```

***

## &#x20;Topic Map - Where Each Topic is Used

| Topic         | Used In                                        |
| ------------- | ---------------------------------------------- |
| Variables     | Step 5 - storing city, temp, humidity          |
| Data Types    | Throughout - int, float, str, bool             |
| Typecasting   | Step 5, 6 - `float()`, `int()` on API values   |
| Operators     | Step 7 - avg calculation                       |
| String        | Steps 2, 5 - f-strings, `.upper()`, `.strip()` |
| Functions     | Every step is a separate function              |
| User Input    | Step 2 (city), Step 8 (filter)                 |
| Conditionals  | Step 5, 6 - alerts logic                       |
| Loops         | Step 6 - looping over forecast days            |
| List          | Step 6 - collecting all max temps              |
| Set           | Step 6 - unique weather conditions             |
| Tuple         | Step 7 - `(min_temp, max_temp)` range          |
| Dictionary    | Steps 3-8 - reading API JSON response          |
| File Handling | Step 4 (JSON), Step 9 (TXT report)             |

***

## &#x20;Sample Output

```
 Enter city name: Kanpur

 Fetching data from API...
 Data fetched successfully!

 Raw data saved → weather_data.json

========================================
 KANPUR, India
========================================
 Temperature  : 38.5°C  (Feels like 41.2°C)
 Humidity     : 45%
 Wind Speed   : 18.7 kph
 Condition    : Sunny
 UV Index     : 9
 UV Alert: Apply sunscreen!

 3-Day Forecast:
----------------------------------------
  2025-05-01
     Max: 39.0°C | Min: 28.0°C | Avg: 33.5°C
     Condition: Sunny | Rain Chance: 5%
     Alert:  Hot Day
  ...

 Forecast Summary:
   Avg Max Temp : 37.5°C
   Temp Range   : 35.0°C – 40.2°C
   Conditions   : {'Sunny', 'Partly Cloudy'}

 Filter days by condition (Sunny / Rainy / Cloudy): sunny
 Days with 'Sunny' condition:
 2025-05-01 → 39.0°C | Sunny

 Report saved → report.txt
```

***

## &#x20;Common Errors & Fixes

| Error               | Reason               | Fix                                           |
| ------------------- | -------------------- | --------------------------------------------- |
| `❌ Error: HTTP 403` | Wrong API Key        | Double check your key on WeatherAPI dashboard |
| `❌ Error: HTTP 400` | Wrong city name      | Check spelling, try English name              |
| `KeyError`          | Wrong dictionary key | Print the full response to see structure      |
| `ConnectionError`   | No internet          | Check your connection                         |

***

## &#x20;Challenge Tasks (Try on Your Own)

1. **Easy:** Also print the local time of the city from the API response
2. **Medium:** Show which day in the forecast has the highest chance of rain
3. **Hard:** Ask the user for 2 cities and compare their current temperatures side by side

***

## 📎 Resources

* WeatherAPI Docs: [https://www.weatherapi.com/docs/](https://www.weatherapi.com/docs/)
* Python `json` module: [https://docs.python.org/3/library/json.html](https://docs.python.org/3/library/json.html)
* Python `urllib`: [https://docs.python.org/3/library/urllib.request.html](https://docs.python.org/3/library/urllib.request.html)
