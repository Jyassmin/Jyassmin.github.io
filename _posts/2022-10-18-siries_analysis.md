---
layout: single
title:  "시계열 예측"
categories: coding
tag: [python, coding]
toc: true
author_profile: true
sidebar:
    nav: "docs"
---

<head>
  <style>
    table.dataframe {
      white-space: normal;
      width: 100%;
      height: 240px;
      display: block;
      overflow: auto;
      font-family: Arial, sans-serif;
      font-size: 0.9rem;
      line-height: 20px;
      text-align: center;
      border: 0px !important;
    }

    table.dataframe th {
      text-align: center;
      font-weight: bold;
      padding: 8px;
    }

    table.dataframe td {
      text-align: center;
      padding: 8px;
    }

    table.dataframe tr:hover {
      background: #b8d1f3; 
    }

    .output_prompt {
      overflow: auto;
      font-size: 0.9rem;
      line-height: 1.45;
      border-radius: 0.3rem;
      -webkit-overflow-scrolling: touch;
      padding: 0.8rem;
      margin-top: 0;
      margin-bottom: 15px;
      font: 1rem Consolas, "Liberation Mono", Menlo, Courier, monospace;
      color: $code-text-color;
      border: solid 1px $border-color;
      border-radius: 0.3rem;
      word-break: normal;
      white-space: pre;
    }

  .dataframe tbody tr th:only-of-type {
      vertical-align: middle;
  }

  .dataframe tbody tr th {
      vertical-align: top;
  }

  .dataframe thead th {
      text-align: center !important;
      padding: 8px;
  }

  .page__content p {
      margin: 0 0 0px !important;
  }

  .page__content p > strong {
    font-size: 0.8rem !important;
  }

  </style>
</head>


# [시계열 예측]

---


# 1. 변동의 종류


- 추세변동(trend variation)

- 순환변동(cyclical variation)

- 계절변동(seasonal variation

- 위 변동요인을 동시에 갖는 변동

- 불규칙변동(irregular variation or random variation)


---


# 2. 평활화 기법

## 1 ) SMA(Smoothing Methods Analysis)


- 단순 이동 평균은 가장 일반적인 평균 유형이다.

- SMA에서는 최근 데이터 포인트의 합계를 수행하고 기간별로 나눈다.

- 슬라이딩 너비의 값이 클수록 데이터가 더 평활해지지만, 값이 크면 정확도가 떨 어질수있다.

- SMA를 계산하기 위해 pandas의 Series.rolling() 메서드를 사용한다.


### a. Apple 주식을 이용한 평활화기법(SMA)



```python
# !pip install finance-datareader   # 설치
# !pip install -U finance-datareader # 업데이트


# S&P 500에 등록된 모든 종목 리스트 가져와서 Apple사의 Symbol확인
import FinanceDataReader as fdr
df_spx = fdr.StockListing('S&P500')
# df_spx.head(3)

df_spx.loc[df_spx["Name"] == "Apple Inc.", ["Name", "Symbol"]]
# df_spx.loc[df_spx["Name"] == "Amazon", ["Name", "Symbol"]]  #아마존 symbol
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Symbol</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>45</th>
      <td>Apple Inc.</td>
      <td>AAPL</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 애플 가격 데이터 가져오기

df_apple = fdr.DataReader(symbol='AAPL', start='2010') # 애플, 2010년~현재
# df_apple.date_range(start="2020-08", periods=8, freq="W")
## start : 시작일, periods : 생성할 날짜의 개수, freq : 생성할 날짜의 주기
df_apple.head(3)
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Close</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
      <th>Change</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2010-01-04</th>
      <td>7.64</td>
      <td>7.62</td>
      <td>7.66</td>
      <td>7.58</td>
      <td>493730000.0</td>
      <td>0.0146</td>
    </tr>
    <tr>
      <th>2010-01-05</th>
      <td>7.66</td>
      <td>7.66</td>
      <td>7.70</td>
      <td>7.62</td>
      <td>601900000.0</td>
      <td>0.0026</td>
    </tr>
    <tr>
      <th>2010-01-06</th>
      <td>7.53</td>
      <td>7.66</td>
      <td>7.69</td>
      <td>7.53</td>
      <td>552160000.0</td>
      <td>-0.0170</td>
    </tr>
  </tbody>
</table>
</div>



```python
import pandas as pd
df_apple["Close"].plot(figsize=(10,6))  # 파랑
df_apple["Close"].rolling(window=30).mean().plot(figsize=(10,6)) # 30일 이동평균(window), 노랑
```

<pre>
<AxesSubplot:xlabel='Date'>
</pre>
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAlYAAAFeCAYAAABHHlHvAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjMuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8vihELAAAACXBIWXMAAAsTAAALEwEAmpwYAABei0lEQVR4nO3dd3zV1f3H8de5K3sQMgh77w0ynODEvXfrat22tdvWWq2jWltb+3Pbat0Dxb03IooIyt4jbEJCQva6957fH9+bBQFCcpObkPfz8eDBd38/9xC4H873fD/HWGsRERERkeZzRToAERERkYOFEisRERGRMFFiJSIiIhImSqxEREREwkSJlYiIiEiYKLESERERCRNPpAMASE1Ntb179450GCIiIiL7NX/+/FxrbVpD+9pEYtW7d2/mzZsX6TBERERE9ssYs2Fv+/QoUERERCRMlFiJiIiIhIkSKxEREZEwUWIlIiIiEiZKrERERETCRImViIiISJgosRIREREJEyVWIiIiImGixEpEREQkTJRYiYiIiISJEisREREJm7vfX87c9XmRDiNilFiJiIhIWASDlsdmruO8x76JdCgRo8RKREREwmJnSWWkQ4g4JVYiIiISFofc9UmkQ4g4JVYiIiLSLK/O30zvm95t9PHBoCUQtC0YUeQosRIREZFm+c0rCw/o+KP+8Tn9/vgeFf5AC0UUOUqsREREpFVtyisD4I53lkU4kvBTYiUiIiIRsXBTQaRDCLv9JlbGmCeNMTuMMUvqbHvZGLMg9CvLGLMgtL23Maaszr5HWzB2ERERaYOOGpjWqON8noOvf6cxn+gpYFrdDdba8621o621o4EZwGt1dq+t3metvSZskYqIiEi7UD0wfeuuMnrf9C53v7+8weOiOmJiZa39EmiwhKoxxgDnAS+GOS4RERFpp75ak8s7i7Zy6D2fAfDYzHUNHud1d8DEaj+OALKttavrbOtjjPnBGDPTGHNEM68vIiIi7cwxrvkMePU4+pkte+wrKKuqWW5KwYXSSj/frtvZjOhaVnMTqwup31u1DehprR0D/Ap4wRiT2NCJxpirjDHzjDHzcnJymhmGiIiItBV3e59gkGsz57pn7rFvbU5xzXJTHgXe9e5yzn98Tr3rtCVNTqyMMR7gLODl6m3W2gpr7c7Q8nxgLTCwofOttY9ba8dba8enpTVu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"/>


```python
df_apple["3M"] = df["Close"].rolling(window=3).mean().diff(1)
df_apple
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Close</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
      <th>Change</th>
      <th>3M</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2010-01-04</th>
      <td>7.64</td>
      <td>7.62</td>
      <td>7.66</td>
      <td>7.58</td>
      <td>493730000.0</td>
      <td>0.0146</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2010-01-05</th>
      <td>7.66</td>
      <td>7.66</td>
      <td>7.70</td>
      <td>7.62</td>
      <td>601900000.0</td>
      <td>0.0026</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2010-01-06</th>
      <td>7.53</td>
      <td>7.66</td>
      <td>7.69</td>
      <td>7.53</td>
      <td>552160000.0</td>
      <td>-0.0170</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2010-01-07</th>
      <td>7.52</td>
      <td>7.56</td>
      <td>7.57</td>
      <td>7.47</td>
      <td>477130000.0</td>
      <td>-0.0013</td>
      <td>-0.040000</td>
    </tr>
    <tr>
      <th>2010-01-08</th>
      <td>7.57</td>
      <td>7.51</td>
      <td>7.57</td>
      <td>7.47</td>
      <td>447880000.0</td>
      <td>0.0066</td>
      <td>-0.030000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2022-10-11</th>
      <td>138.98</td>
      <td>139.90</td>
      <td>141.35</td>
      <td>138.22</td>
      <td>77030000.0</td>
      <td>-0.0103</td>
      <td>-2.150000</td>
    </tr>
    <tr>
      <th>2022-10-12</th>
      <td>138.34</td>
      <td>139.13</td>
      <td>140.36</td>
      <td>138.16</td>
      <td>69830000.0</td>
      <td>-0.0046</td>
      <td>-0.583333</td>
    </tr>
    <tr>
      <th>2022-10-13</th>
      <td>142.99</td>
      <td>134.99</td>
      <td>143.59</td>
      <td>134.37</td>
      <td>112880000.0</td>
      <td>0.0336</td>
      <td>0.856667</td>
    </tr>
    <tr>
      <th>2022-10-14</th>
      <td>138.38</td>
      <td>144.31</td>
      <td>144.52</td>
      <td>138.19</td>
      <td>88240000.0</td>
      <td>-0.0322</td>
      <td>-0.200000</td>
    </tr>
    <tr>
      <th>2022-10-17</th>
      <td>142.41</td>
      <td>141.07</td>
      <td>142.90</td>
      <td>140.27</td>
      <td>84680000.0</td>
      <td>0.0291</td>
      <td>1.356667</td>
    </tr>
  </tbody>
</table>
<p>3221 rows × 7 columns</p>
</div>



```python
df_apple["3M"].plot(figsize=(10,6))
```

<pre>
<AxesSubplot:xlabel='Date'>
</pre>
<img src="data:image/png;base64,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"/>


```python
```
