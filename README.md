import yfinance as yf

# Extracting Tesla stock data
tesla = yf.Ticker("TSLA")
tesla_data = tesla.history(period="max")
tesla_data.reset_index(inplace=True)

# Display the first five rows of the dataframe
print(tesla_data.head())

import requests
from bs4 import BeautifulSoup
import pandas as pd

# Request the webpage
url = "https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue"
html_data = requests.get(url).text

# Parse the HTML content
soup = BeautifulSoup(html_data, "html.parser")

# Extract the table containing revenue data
tables = soup.find_all('table')
tesla_revenue = pd.read_html(str(tables[1]), flavor='bs4')[0]

# Display the last five rows of the dataframe
print(tesla_revenue.tail())

# Extracting GameStop stock data
gamestop = yf.Ticker("GME")
gamestop_data = gamestop.history(period="max")
gamestop_data.reset_index(inplace=True)

# Display the first five rows of the dataframe
print(gamestop_data.head())

# Request the webpage
url = "https://www.macrotrends.net/stocks/charts/GME/gamestop/revenue"
html_data = requests.get(url).text

# Parse the HTML content
soup = BeautifulSoup(html_data, "html.parser")

# Extract the table containing revenue data
tables = soup.find_all('table')
gamestop_revenue = pd.read_html(str(tables[1]), flavor='bs4')[0]

# Display the last five rows of the dataframe
print(gamestop_revenue.tail())

import matplotlib.pyplot as plt

def make_graph(data, title):
    plt.figure(figsize=(10, 5))
    plt.plot(data['Date'], data['Close'])
    plt.title(title)
    plt.xlabel('Date')
    plt.ylabel('Close Price')
    plt.show()

# Plotting Tesla stock data
make_graph(tesla_data, 'Tesla Stock Price')

# Plotting GameStop stock data
make_graph(gamestop_data, 'GameStop Stock Price')

