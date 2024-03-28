# Project Summary
<b>Scraped a data table from wikipedia website and converted it to a csv file.</b>
										<ul>
											<li>Find_all() and find() were implemented with BeautifulSoup library to get the data table in Wikipedia webpage.</li>
											<li>Utilized pandas library to store the scraped data table text into a data frame.</li>
											<li>Implemented for loops and pandas' loc function to record all parsed text.</li>
											<li>Exported data frame  to csv using to_csv().</li>
</ul>

```python
from bs4 import BeautifulSoup
import requests

url = 'https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue'
page = requests.get(url)
soup = BeautifulSoup(page.text , 'html' )

soup.find('table' , class_ = 'wikitable sortable jquery-tablesorter')
#class="wikitable sortable jquery-tablesorter"

#class="wikitable sortable jquery-tablesorter"

soup.find_all('table')[1] 

table = soup.find_all('table')[1] 

print(table)

world_titles = table.find_all('th')

world_titles

world_table_titles = [ title.text.strip() for title in world_titles ]

print(world_table_titles)

import pandas as pd

df = pd.DataFrame(columns = world_table_titles)
df

data_all_rows = table.find_all('tr')

data_all_rows

for row in data_all_rows[1:] :
    row_data = row.find_all('td')
    individual_row_data = [data.text.strip() for data in row_data]
    
    length = len(df)
    df.loc[length] = individual_row_data 

df.set_index('Rank')

df

df.to_csv(r'C:\Users\wodnj\Desktop\Web Scraping and Pandas\Companies.csv')
```
### Source : [Wikipedia](https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue)
