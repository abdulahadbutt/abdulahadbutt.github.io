---
title:  How do you scrape data from a website using python?
date:   2022-10-09 18:16:52 +0500
author: Abdul Ahad Butt
tags: 
    - selenium
    - BeautifulSoup
# desc: 
---

# How to scrape websites?
First lets grab the needed modules

```shell
pip install -U selenium
pip install webdriver-manager
pip install beautifulsoup4
```
<!--more-->
### You might be asking what are these modules?
Here's the run down. 

__selenium__ basically helps us automate browsers! It opens up a browser on your device your python script can interact with. 

__webdriver-manager__ is a wrapper module for selenium. How it works is, selenium needs a "driver" to interface with a chosen browser. Selenium docs has links to where you can download these drivers, however webdriver-manager circumvents this problem by automating the downloading and saving of webdrivers

And finally __beatifulsoup4__ is our chosen html parser. 

## Next create a new file main.py
You can do this manually or by running the below command (only for linux)
```powershell
touch main.py
```

<!-- {% highlight powershell %}
touch main.py
{% endhighlight %} -->

# Now in the file add these lines
<!-- ```python
from selenium import webdriver
from selenium.webdriver.firefox.service import Service as FirefoxService
from webdriver_manager.firefox import GeckoDriverManager

driver = webdriver.Firefox(service=FirefoxService(GeckoDriverManager().install()))
``` -->

{% highlight python %}
from selenium import webdriver
from selenium.webdriver.firefox.service import Service as FirefoxService
from webdriver_manager.firefox import GeckoDriverManager

driver = webdriver.Firefox(service=FirefoxService(GeckoDriverManager().install()))
{% endhighlight %}



# Choose your URL
First lets see which sites we can scrape from
The example rn is olx.com, a pakistani site called olx.com


```python
URL = "https://czone.com.pk/laptops-pakistan-ppt.74.aspx"
driver.get(URL)
```

We can get the page source from the driver and pass it to our html parser
```python
soup = BeautifulSoup(driver.page_source, 'lxml')
products = soup.findAll(
    'div', {'class': 'product'}
)
```


Next lets grab all the products on that page and put them into a list
```python
records = []
for product in products:
    product_name = product.find('h4').getText().strip()
    product_price = product.find('div', {'class': 'price'}).getText().strip()

    records.append((product_name, product_price))
```

