# Crypto-Website-Automation
``` from requests import Request, Session
from requests.exceptions import ConnectionError, Timeout, TooManyRedirects
import json

url = 'https://pro-api.coinmarketcap.com/v1/cryptocurrency/listings/latest' 
# Original Sandbox Environment: 'https://sandbox-api.coinmarketcap.com/v1/cryptocurrency/listings/latest'
parameters = {
  'start':'1',
  'limit':'15',
  'convert':'USD'
}
headers = {
  'Accepts': 'application/json',
  'X-CMC_PRO_API_KEY': '72f476ae-15ca-4651-8193-6c0fc1b3fbfc',
}
session = Session()
session.headers.update(headers)

try:
  response = session.get(url, params=parameters)
  data = json.loads(response.text)
  print(data)
except (ConnectionError, Timeout, TooManyRedirects) as e:
  print(e) 
```
```
import pandas as pd
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', None)
```
```
df = pd.json_normalize(data['data'])
df['timestamp'] = pd.to_datetime('now')
df['date'] = df['timestamp'].dt.strftime('%Y-%m-%d')
df
```
```
# Creating a function to Automate the process

def api_runner():
    global df
    url = 'https://pro-api.coinmarketcap.com/v1/cryptocurrency/listings/latest' 
    # Original Sandbox Environment: 'https://sandbox-api.coinmarketcap.com/v1/cryptocurrency/listings/latest'
    parameters = {
      'start':'1',
      'limit':'20',
      'convert':'USD'
    }
    headers = {
      'Accepts': 'application/json',
      'X-CMC_PRO_API_KEY': '72f476ae-15ca-4651-8193-6c0fc1b3fbfc',
    }
    
    session = Session()
    session.headers.update(headers)
    try:
      response = session.get(url, params=parameters)
      data = json.loads(response.text)
      # print(data)
    except (ConnectionError, Timeout, TooManyRedirects) as e:
      print(e)

    df = pd.json_normalize(data['data'])
    df['timestamp'] = pd.to_datetime('now')
    df['date'] = df['timestamp'].dt.strftime('%Y-%m-%d')
    # Appending the data to the dataframe
    #df2 = pd.json_normalize(data['data'])
    #df2['timestamp'] = pd.to_datetime('now')
    #df2['date'] = df2['timestamp'].dt.strftime('%Y-%m-%d')
    #df = pd.concat([df, df2], ignore_index=False)

    # Transforming the dataframe into a CSV File and then appending data into it
    if not os.path.isfile(r'C:\Users\HP\OneDrive\Desktop\Data Analytics Projects\Crypto Website Automation\CryptoCoinCurrency.csv'):
        df.to_csv(r'C:\Users\HP\OneDrive\Desktop\Data Analytics Projects\Crypto Website Automation\CryptoCoinCurrency.csv',header = True)
    else:
        df.to_csv(r'C:\Users\HP\OneDrive\Desktop\Data Analytics Projects\Crypto Website Automation\CryptoCoinCurrency.csv', mode = 'a', header = False)
```
```
import os
api_runner()
print("API Runner Invoked")
```
```
df3 = pd.read_csv(r'C:\Users\HP\OneDrive\Desktop\Data Analytics Projects\Crypto Website Automation\CryptoCoinCurrency.csv')
df3
```
```
# Changing the notation of displaying larger numbers
pd.set_option('display.float_format', lambda x: f'{x:.5f}')
df3
```
```
df4 = df3.groupby('name', sort=False)[['quote.USD.percent_change_1h','quote.USD.percent_change_24h','quote.USD.percent_change_7d','quote.USD.percent_change_30d','quote.USD.percent_change_60d','quote.USD.percent_change_90d']].mean()
df4
```
```
# Pivoting the DataFrame
df5 = df4.stack()
#Converting the Series to DataFrame
df6 = df5.to_frame(name = 'values')
df6
```
```
df6.count()
```
```
index = pd.Index(range(138))  # Creating a new index
df7 = df6.reset_index()  # Reset old index, keeping it as a column
df7.index = index 
df7
```
