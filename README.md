
## SCRAPING YOUTUBE COMMENTS AND THEIR USERNAME


In real life we cannot expect always to have the whole dataset in our table, most of the time  we need to extract them from the internet itself. So, i thought that youtube comments are also a great source of data which are available publicly and can be extracted. In this project, I scrapped comments and the username  from a youtube video and stored it in a excel file.

This is the video from which i scrapped the comments : https://www.youtube.com/watch?v=uB5bf7LQPVU


## Installation

First  we will  install all the needed library for this project

```bash
  pip install pandas
  pip install time
  pip install selenium

We also need to  install a ChromeDriver and should have google chrome in our PC.
```
## IMPORTING THE LIBRARIES AND MODULES
```
import time
import pandas as pd 
from selenium.webdriver import Chrome
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
```
Here we are using selenium because youtube uses javascript rendering and Beautiful soup cannot handle that, it's the browser that reads and runs that javascript.

## The loop

``` 
Names=[]
comments=[]

driver = Chrome(r'C:\webdrivers\chromedriver.exe') 
wait = WebDriverWait(driver,10)                    
driver.get("https://www.youtube.com/watch?v=uB5bf7LQPVU") 

for item in range(6):  
    wait.until(EC.visibility_of_element_located((By.TAG_NAME, "body"))).send_keys(Keys.END)  
    time.sleep(4) 
```
* driver has the path of chromedriver and with get() function we will access the URL that we want,
* WebDriverWait(driver,10) waits up to 10 seconds before throwing a TimeoutException,  
* The range is set to 6 so it will scroll down 6 times.
* sleep() is set to 4 so that the page will wait for 4 seconds to load 

## FINDING ALL THE ELEMENTS AND APPENDING THEM 





![App Screenshot](https://user-images.githubusercontent.com/99939493/181934991-714dbd6c-bcbe-4853-acd6-de627fd9dade.png)



![App Screenshot](https://user-images.githubusercontent.com/99939493/181935035-399f03be-6cd6-4bbd-b788-515f2c5ca156.png)

As you can see above, to scrape the comments we need to find all the  #content-text elements and # author-text for names.

``` 
for users in wait.until(EC.presence_of_all_elements_located((By.CSS_SELECTOR, "#author-text"))):  
    Names.append(users.text)
            
for comment in wait.until(EC.presence_of_all_elements_located((By.CSS_SELECTOR, "#content-text"))):  
    comments.append(comment.text)
```

## COVERTING THE DATA INTO A DATAFRAME 
```
df=pd.DataFrame(data={"NAMES":Names,"Comments":comments}) 
df
```
Here, I have scrolled down six times by setting the range at 6 and scraped 120 names and their comments 


![App Screenshot](https://user-images.githubusercontent.com/99939493/181935473-2a5a2518-cf94-4504-9000-61b6a652195d.png)

## STORING THE DATA INTO A EXCEL

```
df.to_excel("comments.xlsx") 
```
This file is available in my repository

![App Screenshot](https://user-images.githubusercontent.com/99939493/181935806-e8846d03-4e2f-47a1-aa86-7d03c8f818ee.png)


## THANK YOU ! I HOPE YOU LIKED IT !


## 🚀 About Me
I'm a Student who is learning about Data and continously upgrading my skills with new tech tools and trying to make some projects using them.


## 🔗 Links
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/anuj-rawat-419aa91b5)

[![Medium](https://img.shields.io/badge/Medium-black?style=for-the-badge&logo=medium&logoColor=white)](https://medium.com/@anujrawatacer/naukri-com-raw-data-analysis-using-python-5ead95a04fa9)


