# 🏭 Supply Chain Management-Demand forecasting
This project demonstrates multiple forecasting techniques ranging from basic statistical models to advanced machine learning approaches using Excel and Python.

## Contents 📖
- [Definition](#definition)
- [Types of Demand Forecasting](#types-of-demand-forecasting)
- [Common Demand Forecasting Techniques](#common-demand-forecasting-techniques)
- [Applications in Business](#applications-in-business)
- [1 Qualitative Forecasting](#1-qualitative-forecasting)
- [2 Simple Moving Average](#2-simple-moving-average)
- [3 Weighted Moving Average](#3-weighted-moving-average)
- [4 Exponential Smoothing](#4-Exponential-smoothing)
- [5 Holt Winters](#5-Holt-Winters)
- [6 ARIMA OR SARIMA](#6-ARIMA-OR-SARIMA)
- [7 Regression](#7-Regression)
- [8 Machine Learning](#8-Machine-Learning)
- [Interview Questions](#interview-questions)

## Definition

Demand forecasting is the process of predicting future customer demand for a product or service using historical data, statistical models and machine learning techniques. It helps businesses optimize inventory, production, pricing anf supply chain management.

## Types of Demand Forecasting
1. *Qualitative Forecasting:* Based on expert opinions, market research and surveys (useful for new produts).
2. *Time Series Forecasting:* Uses historical data and statistical methods like moving averages, exponential smoothing and ARIMA.
3. *Casual Forecasting:* Considers external factors like economic indicators, pricing, promotions and competitor strategies.
4. *Machine Learning-Based Forecasting:* Uses algorithms like XGBoost, LSTMs and regression models to predict demand.

## Common Demand Forecasting Techniques
- **Moving Averages** - Simple, Weighted, Exponential
- **ARIMA** - AutoRegressive Integrated Moving Average
- **SARIMA** - Seasonal Smoothing
- **Holt-Winters Exponential Smoothing**
- **Regression Analysis**
- **Machine Learning Models** - Random Forest, XGBoost, LSTMs etc.

## Applications in Business
- **Inventory Management:** Prevents stockouts and overstocking
- **Supply Chain Optimization:** Ensures a smooth flow of goods.
- **Financial Planning:** Helps in budgeting and resource allocation.
- **Production Scheduling:** Aligns manufacturing with expected demand.
- **Pricing Strategy:** Supports dynamic pricing decisions.

## Examples
### 1 Qualitative Forecasting 
- (Expert/Judgment Bases)
  
**Scenario:** A logistics company is launching same-day delivery in Tier-2 cities. There is no historical data, so demand is estimated using:
- Sales team input
- City population
- Past launches in similar cities

**📊 Excel Method**
- Create assumptions tables:
  
| **City** | **Expected Orders/Day** |
|-----------------|---------------|
| Indore    | 1200          |
| Surat   | 1500       |
| Jaipur        | 1800      |

- Use **AVERAGE/WEIGHTED AVERAGE** based on expert confidence
- Final demand = weighted estimate

**👨‍💻 Python Method**
```python
import pandas as pd
data = {
        'City' : ['Indore','Surat','Jaipur']
        'Expected_Demand' : [1200,1500,1800]
}

df = pd.DataFrame(date)
df
```

#### Use When
- New service/new city
- No historical data

### 2 Simple Moving Average 
- (Time Series)

**Scenario:** Forecast daily parcel volume for next week using last 7 days data.

**📊 Excel Method**
```excel
= AVERAGE(B2:B8)
```

| **Date** | **Orders** |
|-----------------|---------------|
| Day 1   | 8000     |
| Day 2   | 8200     |
| Day 3   | 7900     |
| Day 4   | 8100     |
| Day 5   | 8300     |
| Day 6   | 8500     |
| Day 7   | 8400     |

**-> Forecast = Average of last 7 days**

**👨‍💻 Python Method**
```python
import pandas as pd

orders = [8000,8200,7900,8100,8300,8500,8400]
df = pd.DataFrame({'orders': orders])

forecast = df['orders'].rolling(window=7).mean().iloc[-1]
forecast
```

#### Use When
- Stable demand
- No seasonality

### 3 Weighted Moving Average
**Scenerio:** Recent days matter more due to sale season.

**📊 Excel Method**
```excel
=SUMPRODUCT(B2:B8,{0.05,0.1,0.15,0.2,0.2,0.15,0.15})
```

**👨‍💻 Python Method**
```python
weights = [0.05,0.1,0.15,0.2,0.2,0.15,0.15]
forecast = sum(w*d for w,d in zip(weights, orders))
forecast
```

#### Use When
- Recent demand is more important

### 4 Exponential Smoothing
**Scenerio:** Forecast parcel demand where demand changes gradually.

**📊 Excel Method**
```excel
Forecast = α*Actual + (1-α)*Previous Forecast
```
Example:
- α = 0.3

**👨‍💻 Python Method**
```python
from statsmodels.tsa.holtwinters import SimpleExpSmoothing

model = SimpleExpSmoothing(orders)
fit = model.fit(smoothing_level=0.3)
fit.forecast(1)
```

#### Use When
- Short-term forecasting
- Smooth trend

### 5 Holt Winters
- Trend + Seasonality
**Scenerio:** Logistics company sees weekly sesonality:
- High orders on Fri-Sun
- Low on Mon-Tue

**📊 Excel Method**
- Use Data -> Forecast Sheet
- Select seasonality = 7

**👨‍💻 Python Method**
```python
from statsmodels.tsa.holtwinters import ExponentialSmoothing

model = ExponentialSmoothing(
 orders,
 trend='add',
 seasonal='add',
 seasonal_periods=7
)

fit = model.fit()
fit.forecast(7)
```

#### Use When
- Trend + Seasonality exist

### 6 ARIMA OR SARIMA
**Scenerio:** Forecast monthly shipment volume considering long-term trend and seasonality.

**📊 Excel Method**
- Limited support
- Usually avoided for ARIMA

**👨‍💻 Python Method**
```python
from statsmodels.tsa.arima.model import ARIMA

model = ARIMA(orders, order=(1,1,1))
fit = model.fit()
fit.forecast(steps=7)
```

#### Use When
- Strong time-series patterns
- Medium-logn term planning

### 7 Regression
- Causal Forecasting

**Scenerio:** Demand depends on -
- Discounts
- Marketing spend
- Delivery fee

**📊 Excel Method**
- Data -> Data Analysis -> Regression
- Dependent: Orders
- Independent: Discount%, Ad Spend

**👨‍💻 Python Method**
```python
from sklearn.linear_model import LinearRegression

x = [[10, 50000], [15, 70000], [20, 90000]]
y = [8000, 10000, 13000]

model = LinearRegression()
model.fit(x,y)
model.predict([[18, 80000]])
```

#### Use When
- External factors affect demand

### 8 Machine Learning
- (XGBoost/Randon Forest)

**Scenerio:** Forecast city-level daily demand using-
- Day of Week
- Festival flag
- Weather
- Discounts

**📊 Excel Method**
❌ Not suitable

**👨‍💻 Python Method(Random Forest)**
```python
from sklearn.ensemble import RandomForestRegressor

x = [[1,0,10],[2,1,15],[3,0,20]]
y = [8000, 12000, 15000]

model = RandomForestRegressor()
model.fit(x,y)
model.predict([[4,1,18]])
```

#### Use When
- Large data
- Non-linear patterns













