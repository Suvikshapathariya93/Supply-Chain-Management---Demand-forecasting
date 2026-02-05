# 🏭 Supply Chain Management-Demand forecasting

## Contents 📖
- [Definition](#definition)
- [Types of Demand Forecasting](#types-of-demand-forecasting)
- [Common Demand Forecasting Techniques](#common-demand-forecasting-techniques)
- [Applications in Business](#applications-in-business)
- [Qualitative Forecasting](#qualitative-forecasting)
- [Simple Moving Average](#simple-moving-average)
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
### Qualitative Forecasting 
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

### Simple Moving Average 
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







