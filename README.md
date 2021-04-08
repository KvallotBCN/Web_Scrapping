# Web_Scrapping
## A repository having my tests on Web Scrapping



### Test1: We are doing a test to scrap information from a website:

import requests

#import requests module and beautifulsoup via the command in my console (CMD) pip install package_name

from bs4 import BeautifulSoup


#Beautiful Soup is a library that makes it easy to scrape information from web pages.
#It sits atop an HTML or XML parser, providing Pythonic idioms for iterating, searching, and modifying the parse tree.


###### Product page url:
url = "http://books.toscrape.com/catalogue/full-moon-over-noahs-ark-an-odyssey-to-mount-ararat-and-beyond_811/index.html"
print("L'url est: " + url)

reponse = requests.get(url)

#I created a variable called reponse to check if the connection between the url and my script is good (code 200) or not (code 400, 500 etc...)

print(reponse)

#Reponse is 200 so the link is done. 

if reponse.ok:
    print(reponse.text)

#On pourrait iterer par mot mais c'est pas pratique donc on va plutot le parser.
#Pour parser on va créer une variable qui imprime le texte de la page htlm du site web.

if reponse.ok :
    soup = BeautifulSoup(reponse.text , "lxml")

##### Titre:
    title = soup.title.string
    print("Le titre est: " + title)



    Image_url = soup.find("img").get("src")
    print(Image_url)
    
   
os.system ("pause")
