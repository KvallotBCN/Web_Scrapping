# Web_Scrapping
# A repository having my tests on Web Scrapping



# Test1: We are doing a test to scrap information from a website:

import requests

# import requests module and beautifulsoup via the command in my console (CMD) pip install package_name

from bs4 import BeautifulSoup


# Beautiful Soup is a library that makes it easy to scrape information from web pages.
# It sits atop an HTML or XML parser, providing Pythonic idioms for iterating, searching, and modifying the parse tree.


# Product page url:
url = "http://books.toscrape.com/catalogue/full-moon-over-noahs-ark-an-odyssey-to-mount-ararat-and-beyond_811/index.html"
print("L'url est: " + url)

reponse = requests.get(url)

# I created a variable called reponse to check if the connection between the url and my script is good (code 200) or not (code 400, 500 etc...)

print(reponse)

# Reponse is 200 so the link is done. 

if reponse.ok:
    print(reponse.text)

# On pourrait iterer par mot mais c'est pas pratique donc on va plutot le parser.
# Pour parser on va créer une variable qui imprime le texte de la page htlm du site web.

if reponse.ok :
    soup = BeautifulSoup(reponse.text , "lxml")
    print(soup)

#Finding meta tag containing the content description of the book and print it. 

    meta_tag_content = soup.findAll('meta' , content_="")
    print(meta_tag_content)


    title = soup.title.string
    print("Le titre est: " + title)
# Si on veut le titre sans les balises il faut ajouter .text a title dans le print.

# on doit indiquer l'element parser (lmxl dans ce cas ci) pour que beautifulsoup le sache sinon il y a un warning qui apparait.
    
# Les TR sont des colonnes dans le html texte et les TD sont des cellules. TDS est le pluriel de td. 

# on peut chercher un element grace a la fonction .find(elemenbt css). Dans ce cas ce sera la balise <title>.

    table_data = soup.find("table" , attrs={"class": "table table-striped"})
    print(table_data)
# OU chercher par ligne chaque information. Pour cela, il faut chercher le tr qui a une certaine classe sous le format dictionaire "clé: valeur".

    



# Chercher la premiere image de la page qui est l'image du livre et prendre uniquement l'url de l'image. Les six autres url image de la page sont les urls des livres dans "Products you recently viewed".

    Image_url = soup.find("img").get("src")
    print(Image_url)
