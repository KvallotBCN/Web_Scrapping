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



##### Table:
    Table = soup.find(attrs={"class": "table table-striped"}) 

#####UPC:

    UPC = Table.contents[1]
    print("The UPC of the Book is : " + UPC.text)
    print()

#####Product_Type:

    Line_with_Product_type_in_Website = UPC.find_next("tr")
    Ref_Product_type = Line_with_Product_type_in_Website.find("td")
    print("The type of the product is : " + Ref_Product_type.text)
    print()

#####Price without Tax:

    Line_with_Price_sin_tax_in_Website = Line_with_Product_type_in_Website.find_next("tr")
    Price_sin_tax = Line_with_Price_sin_tax_in_Website.find("td")
    print("The price of the Book without taxes is " + Price_sin_tax.text)
    print()
    
#####Price with Tax:

    Line_with_Price_with_tax_in_Website = Line_with_Price_sin_tax_in_Website.find_next("tr")
    Price_with_tax = Line_with_Price_with_tax_in_Website.find("td")
    print("The price of the Book with taxes is " + Price_with_tax.text)
    print()

#####Tax:

    Line_Tax_in_Website = Line_with_Price_with_tax_in_Website.find_next("tr")
    Tax = Line_Tax_in_Website.find("td")
    print("The tax applied on this book is  " + Tax.text)
    print()

#####Stock:

    Line_Stock_in_Website = Line_Tax_in_Website.find_next("tr")
    Stock = Line_Stock_in_Website.find("td")
    print("Availability of the book = " + Stock.text)
    print()

#####Number reviews:

    Line_Number_reviews_in_Website = Line_Stock_in_Website.find_next("tr")
    Number_reviews = Line_Number_reviews_in_Website.find("td")
    print("Number of reviews about this book are " + Number_reviews.text)
    print()

#####Description of the Book:

    print("The Descrition of the Book : ")
    page = soup.find(attrs={"id": "product_description"})
    paragraph = page.find_next("p")
    print(paragraph.text)
    print()
   

 Chercher le paragraphe du Product description:

 pour paragraph dans l'url donné chercher tous les p
 Si la longueur de p est de plus de quelques mots, imprimer p.

###### The Category of where is located the Book: 

    url_top_page = soup.findAll("ul" , attrs={"class": "breadcrumb"})
    for urls in url_top_page :
        category_url = urls.contents[5]
        Only_Text_Category = category_url.text
        print("The category of this book is: " + Only_Text_Category)
        
    


Chercher la premiere url de chaque page qui est l'image du livre. Les six autres url sont les urls des livres dans "Products you recently viewed".
L'URL n'est pas entière, il faut donc utiliser "from urllib.parse import urljoin" qui permet de joindre la base de url avec le reste de l'url et donc de l'avoir entiere. 
###### Image URL:

    Image_url = soup.find("img").get("src")
    base_url = "http://books.toscrape.com/.html"
    href = Image_url
    print ("The image url is: " + urljoin (base_url, href))
    print()

   
os.system ("pause")
