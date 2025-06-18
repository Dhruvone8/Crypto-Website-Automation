
# 📈 Crypto Website Automation

This project automates the process of fetching real-time cryptocurrency data using the CoinMarketCap API, saving it to a CSV file, and analyzing the percent change of coin prices over various time intervals.

## 🚀 Features

- Fetches the latest cryptocurrency listings from CoinMarketCap API
- Saves the data into a CSV file (appends on subsequent runs)
- Formats timestamps and dates
- Reads and aggregates historical data
- Calculates average percent changes over various periods
- Prepares the data for further visualization and analytics

## 📂 Project Structure

```
Crypto-Website-Automation/
│
├── Code.md              # Code for data fetching, storing, and analysis
├── CryptoCoinCurrency.csv  # CSV file where data is stored (generated at runtime)
└── README.md            # Project documentation (this file)
```

## 🛠 Requirements

- Python 3.x
- Libraries:
  - `requests`
  - `pandas`
  - `json`
  - `os`

Install dependencies via:

```bash
pip install requests pandas
```

## 🔐 API Key

Replace the placeholder API key in the script with your own from [CoinMarketCap Developer Portal](https://coinmarketcap.com/api/).

```python
headers = {
  'Accepts': 'application/json',
  'X-CMC_PRO_API_KEY': 'your_api_key_here',
}
```

## 🧪 Usage

1. Run the script to invoke the API and save data:

```python
api_runner()
```

2. Read the stored CSV:

```python
df = pd.read_csv('path_to_csv')
```

3. Perform analysis like mean percent changes and pivoting for visualization.

## 📊 Analysis Output

- Average percent changes:
  - 1h
  - 24h
  - 7d
  - 30d
  - 60d
  - 90d

- Data is grouped and transformed into a format suitable for plotting or reporting.

## 📌 Notes

- The current implementation uses absolute file paths. Consider modifying them for portability:
  ```python
  os.path.join(os.getcwd(), 'CryptoCoinCurrency.csv')
  ```

- CSV file is appended to with each API call. Avoid running too frequently to prevent data redundancy.

## 📄 License

This project is for educational and non-commercial use. API terms apply.
