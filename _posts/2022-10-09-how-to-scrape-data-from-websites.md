---
layout: post
title:  How do you scrape data from a website using python?
date:   2022-10-09 18:16:52 +0500
author: Abdul Ahad Butt
tags: selenium,BeautifulSoup
# desc: 
---

# How to scrape websites?
First lets grab the needed modules

```shell
pip install -U selenium
pip install webdriver-manager
pip install beautifulsoup4
```


## Next create a new file main.py
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

