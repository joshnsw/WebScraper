# WebScraper

<b>Description:</b>
In this project, I utilized a python webscraper library to scrap information from amazon page,allowing me to track the price of a product that I am interested in.


<b>What I learnt:</b>
I learnt the basics of web scraping,and the valuable data that can be obtained of using this technology. Web scraping tools enable the user to track all sorts of information on the internet,and in a business context, allows the user to extract business-related data(product price,important announcements) from a competitor's website which can be important information when formulating internal business strategy.


<b>Details of the project:</b>

![Screenshot](https://github.com/joshnsw/WebScraper/blob/main/amazon.png)

For this project i used python library 'Beautiful Soup' to parse the html information of this page,to obtain the price information of the product.

The steps for this projects are as follows:

1.Parse the html through beautifulsoup
2.Get the information you want by specifiying the html tag info (in this case the id of the product title which contains the product price)
3.create a csv file to store price info with date.
4.Create a function to add daily price data to the csv file.

```
def price_checker():

URL = 'https://www.amazon.co.jp/-/en/Panasonic-VE-GD27-W-Equipped-Anti-Spunk-Function/dp/B09CKYRYGF/ref=sr_1_5?crid=1C3D898SBTK6X&keywords=%E9%9B%BB%E8%A9%B1&qid=1654318184&sprefix=phon%2Caps%2C188&sr=8-5'

headers= {"User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.3 Safari/605.1.15"};

page = requests.get(URL,headers= headers)

Soup1 = BeautifulSoup(page.content,"html.parser")

SoupPretty = BeautifulSoup(Soup1.prettify(),"html.parser")

titleFind = SoupPretty.find(id='productTitle').get_text()

priceFind = SoupPretty.find(class_='a-offscreen').get_text()


price = priceFind.strip()[1:]
title = titleFind.strip()

import datetime
today = datetime.date.today()

header = ['Title','Price','Date']
data = [title,price,today]


with open('AmazonWebScraperDataset.csv','a+',newline='',encoding='UTF8') as f:
    writer = csv.writer(f)

    writer.writerow(data)


While(True):
    price_checker()
    time.sleep(86400)

```





