# Selenium_coletar_links_youtube
 Pequeno codigo em Seleium para acessar, pesquisar e coletar links de videos no  Youtube. 
 
 ```python
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.options import Options
from webdriver_manager.chrome import ChromeDriverManager
from selenium import webdriver
import pandas as pd
import time

options = Options()
options.add_argument("start-maximized")

driver = webdriver.Chrome(ChromeDriverManager().install())
chrome_options = webdriver.ChromeOptions()

driver.get("http://youtube.com")
 ```

 
 
 ![image](https://user-images.githubusercontent.com/33934341/195915245-013eb9b4-fd78-4988-ae50-7393b421307c.png)
 
 
 ![image](https://user-images.githubusercontent.com/33934341/195915870-adcb35a3-0e4c-4d61-8fc7-2594f3fc651b.png)




```python
busca  = "Python e Django"
driver.find_element(By.NAME, "search_query").click()
driver.find_element(By.NAME, "search_query").send_keys(busca, Keys.ENTER)

time.sleep(2)

videos = driver.find_elements(By.ID, "video-title")

lista_df = []
for video in videos:
    lista_apoio = []
    link = video.get_attribute("href")
    titulo = video.get_attribute("title")
    if link == None:
        continue
    lista_apoio.append(link)
    lista_apoio.append(titulo)
    lista_df.append(lista_apoio)
    
df = pd.DataFrame(lista_df, columns=["Links", "Tituulo"])
df.to_excel("Aula.xlsx", index = False)
print("Arquivos Xlsl criado com Sucesso!!")
```
