# ✈️ Airline Performance Dashboard – Detailed Code Explanation

## 📌 Overview

This project is an interactive web dashboard built using **Dash** and **Plotly**. It allows users to analyze **US domestic airline performance and delay data** by selecting a report type and year.

---

## 🧰 Libraries Used

```python
import pandas as pd
import dash
from dash import Dash, html, dcc
from dash.dependencies import Input, Output, State
import plotly.express as px
```

### Explanation:

* **pandas** → Used for data manipulation and analysis
* **dash** → Framework to build web applications in Python
* **html, dcc** → Dash components for UI (text, dropdowns, graphs)
* **Input, Output, State** → Used for interactivity (callbacks)
* **plotly.express** → Used for creating interactive charts

---

## 🚀 App Initialization

```python
app = Dash(__name__)
app.config.suppress_callback_exceptions = True
```

### Explanation:

* Initializes the Dash app
* `suppress_callback_exceptions=True` allows callbacks for components that are created dynamically

---

## 📊 Data Loading

```python
airline_data = pd.read_csv('URL', encoding="ISO-8859-1")
```

### Explanation:

* Loads dataset from an online source
* Encoding ensures proper reading of special characters

---

## 📅 Year Selection List

```python
year_list = list(range(2005, 2021))
```

### Explanation:

* Creates a list of years for dropdown selection

---

## 🔍 Data Processing Functions

### 1️⃣ Performance Data

```python
def compute_data_choice_1(df):
```

This function prepares data for **Performance Report**.

#### Outputs:

* **Bar Data** → Flight cancellations by month
* **Line Data** → Average airtime per airline
* **Pie Data** → Diverted flights
* **Map Data** → Flights by origin state
* **Tree Data** → Flights by destination and airline

---

### 2️⃣ Delay Data

```python
def compute_data_choice_2(df):
```

This function prepares data for **Delay Report**.

#### Outputs:

* Carrier Delay
* Weather Delay
* NAS Delay
* Security Delay
* Late Aircraft Delay

(All averaged monthly per airline)

---

## 🖥️ Application Layout

```python
app.layout = html.Div([...])
```

### Components:

### 🏷️ Title

```python
html.H1("US Domestic Airline Flights Dashboard")
```

---

### 🔽 Dropdown 1: Report Type

```python
dcc.Dropdown(id='input-type', options=[...])
```

Options:

* Performance Report
* Delay Report

---

### 🔽 Dropdown 2: Year Selection

```python
dcc.Dropdown(id='input-year', options=[...])
```

---

### 📈 Output Container

```python
html.Div(id='output')
```

* This is where graphs will be displayed dynamically

---

## 🔁 Callback Function (Core Logic)

```python
@app.callback(Output('output','children'),
              [Input('input-type','value'),
               Input('input-year','value')])
```

### Purpose:

* Updates dashboard when user selects:

  * Report Type
  * Year

---

## ⚙️ Callback Logic

### Step 1: Input Validation

```python
if not chart or not year:
    return "Please select both options"
```

---

### Step 2: Filter Data

```python
df = airline_data[airline_data['Year'] == int(year)]
```

---

### Step 3: Generate Graphs

### 📊 Performance Report (OPT1)

Charts created:

* Bar Chart → Flight cancellations
* Line Chart → Average airtime
* Pie Chart → Diverted flights
* Choropleth Map → Flights by state
* Treemap → Flights by airline & destination

---

### ⏱️ Delay Report (OPT2)

Charts created:

* Carrier Delay
* Weather Delay
* NAS Delay
* Security Delay
* Late Aircraft Delay

(All displayed as line charts)

---

## ▶️ Running the Application

```python
if __name__ == '__main__':
    app.run(debug=True)
```

### Explanation:

* Starts the Dash server
* `debug=True` enables live updates during development

---

## 🌐 How It Works

1. User selects report type
2. User selects year
3. Callback function triggers
4. Data is filtered and processed
5. Graphs are generated dynamically
6. Dashboard updates instantly

---

## 🎯 Key Features

* Interactive dashboard
* Real-time filtering
* Multiple visualization types
* Clean and modular code
* Easy to extend

---


--

Created as a data visualization project using Dash & Plotly.

