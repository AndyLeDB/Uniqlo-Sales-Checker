import requests
from bs4 import BeautifulSoup
headers = {"User-Agent": 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.88 Safari/537.36'}


def check_prices():
#Array containing URLS to have their prices scraped
    URL = [
        'https://www.uniqlo.com/us/en/edo-ukiyo-e-utagawa-kuniyoshi-long-sleeve-sweatshirt-425638.html?dwvar_425638_color=COL56&cgid=men-sweatshirts-and-sweatpants',
        'https://www.uniqlo.com/us/en/men-premium-lambswool-crew-neck-long-sleeve-sweater-419198.html?dwvar_419198_color=COL06#start=16&cgid=men-sweaters',
        'https://www.uniqlo.com/us/en/men-sweatpants-413435.html?dwvar_413435_color=COL09',
        'https://www.uniqlo.com/us/en/men-long-sleeve-hooded-sweatshirt-418705.html?dwvar_418705_color=COL09&cgid=',
        'https://www.uniqlo.com/us/en/men-slim-fit-chino-flat-front-pants-418916.html?dwvar_418916_color=COL09&cgid=',
        'https://www.uniqlo.com/us/en/men-soft-touch-v-neck-long-sleeve-t-shirt-418697.html?dwvar_418697_color=COL04&cgid=men-t-shirts#start=11&cgid=men-t-shirts']

#Grabs each URL and scrapes the item name and price
    for eachURL in URL:
        page = requests.get(eachURL, headers=headers)
        soup = BeautifulSoup(page.content, 'html.parser')
        title = soup.find(class_="product-name").get_text()
#Uniqlo designed their website so that if there are sales, there will be a new price next to the original.
#If there is no sale, BeautifulSoup will not be able to find the corresponding sales price and will display an error.
        try:
            check_sale = soup.find(class_="price-sales pdp-space-price").get_text()
        except Exception:
            print("No Sale on item: " + title)
        else:
            sales_price = soup.find(class_="price-sales pdp-space-price").get_text()
            reg_price = soup.find(class_="price-standard pdp-space-price").get_text()
            converted_SalesPrice = float(sales_price)
            converted_RegPrice = float(reg_price)
#If item is on sale and sale is more than 30% of original price, will notify to buy the item, otherwise wallet is safe for the time being
            if (converted_RegPrice - (converted_RegPrice * 30) / 100) < converted_SalesPrice:
                print(title + " is on sale: " + sales_price + ", buy now while its hot!!")
            else:
                print("Sale on item: " + title + " is still expensive, " + sales_price + " don't buy!")

check_prices()
