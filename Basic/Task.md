# Capstone Task

## Overview
Design an ETL (Extract, Transform, Load) process that has 4 phrases in every predefined time t (for example 10 minutes). Starting crawl data from [Books to Scrape](https://books.toscrape.com/), process the data in parallel, and update it into MongoDB and PostgreSQL based on the following conditions:

### Data Crawling Conditions
- **First Phrase:**
  - Extract books whose titles start with letters **A to H**.
  - Filter books with a price **higher than the average price of all of these books**, tag it with 'elite_price'.
  - The other books will be tagged as 'scrap_price'.
  - Store the data in the **Book collection of MongoDB**.
  
- **Second Phrase:**
  - Extract books whose titles start with letters **I to Z**.
  - Filter books with a **rating higher than 2 stars**, tag it with 'elite_rate'
  - The other books will be tagged as 'scrap_rate'
  - Store the data in **PostgreSQL**.

- **Third Phrase** 
  - Extract books which has highest price in every genre
  - Save the data in **MongoDB**

- **Fourth Quater**
  - Using function random, auto update the price and the star of a these books.


### Search API
Using the defined databases, implement a simple **search API** utilizing the **BM25 ranking function** to find books with the most relevant descriptions based on the input query.

#### Example Usage:
```python
query = 'shirts, pants, socks'

search = SearchAPI()
result = search(query)

print(result)

## Expected output

[
    {"bookName": "Spark Joy: An Illustrated Master Class on the Art of Organizing and Tidying Up", "score": 0.8},
    {"bookName": "The Art Forger", "score": 0.6},
    ...
]

```