# Analysis of Water Tank Prices in Kenya 

## Background: 
In Kenya, water scarcity is a significant challenge, making water storage solutions such as water tanks critical for both residential and commercial use. Various brands offer water tanks of different sizes and prices. However, consumers often face difficulties in selecting the most cost-effective and reliable water tanks due to the wide range of available options.

## Objective:
The objective of this analysis is to understand the pricing patterns of water tanks in Kenya across different brands and sizes. By analyzing the data on water tank prices, sizes, and brands, I aim to provide insights that can help consumers make informed purchasing decisions.

## Key questions: 

1. What is the price range for each brand?
2. How does tank size affect price?
3. Which brand offers the cheapest tanks for a given size?
4. What is the distribution of tank sizes?
5. Is there a significant difference in prices between brands?
6. What are the most and least expensive brands on average?
7. Which brand offers the best value for money based on price per liter?

## Data collection

I shall apply web scrapping method using **Python** to get the data from a webpage.

```python
import requests
from bs4 import BeautifulSoup
import pandas as pd

#URL of the page to scrape
url = ''

#Send a GET request to the page
response = requests. get(url)

#Parse the page content
soup = BeautifulSoup(response.content,'html.parser')

#Find the table in the page assuming the table is in a apecific class or id
table = soup.find ('table')

#Initialize lists to store the data
sizes = []
brands = []
prices = []

#Extract table rows
rows = table. find_all('tr')
for row in rows[1:]: #skip the header row
    cells = row.find_all('td')
    if len(cells) == 3:
        size = cells [0].text.strip ()
        brand = cells [1].text.strip()
        price = cells [2].text.strip ()

        sizes.append(size)
        brands.append(brand)
        prices.append(price)

#Create a DataFrame
data = {
'Size (Litres)' : sizes,
'Brand' : brands,
'Prices (Kshs)' : prices
}
df = pd.DataFrame(data)

#Optionally, save the DataFrame to a csv file
df.to_csv('Water_tank_prices_Kenya. csv', index = False)
```

## Data Quality Check 

### a. Check missing values
