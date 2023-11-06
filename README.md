# BizCardX-Extracting-Business-Card-Data-with-OCR
## BizCardX: Extracting Business Card Data with OCR using technologies OCR,streamlit GUI, SQL,Data Extraction with Python
## Table of Contents
- [Introduction](#introduction)
- [Problem_statement ](#Problem_statement)
- [Libraries](#Libraries)
- [Problem_solution](#Problem_solution)
- [Conclusion](#Conclusion)
# Introduction:
- BizCardX: Extracting Business Card Data with OCR Overview BizCardX is a Streamlit web application which extracts data from business cards using Optical Character Recognition (OCR). Users can upload an image of a business card and the application uses the easyOCR library to extract relevant information from the card. The extracted information is then displayed in a user-friendly format and can be stored in a PostgreSql database for future reference.
# Problem_statement:
- developing a Streamlit application that allows users to upload an image of a business card and extract relevant information from it using
easyOCR. The extracted information should include the company name, card holdername, designation, mobile number, email address, website URL, area, city, state,and pin code. The extracted information should then be displayed in the application's graphical user interface (GUI).
In addition, the application should allow users to save the extracted information intoa database along with the uploaded business card image. The database should be able to store multiple entries, each with its own business card image and extracted information.
- Techonlgies used:Python, Streamlit, easyOCR, and a database
management system like SQLite or MySQL or PostgreSQL.
- The application should have a simple and intuitive user interface that guides users through the process of uploading the business card image and extracting its information. The extracted information should be displayed in a clean and organized manner, and users should be able to easily add it to the database with the click of a button. And Allow the user to Read the data,Update the data and Allow the user to delete the data through the streamlit UI
# Libraries
### Libraries/Modules needed for the project!
- Streamlit - (To Create Graphical user Interface)
- Psycopg2 - (To Create local database and interact with data)
- Json - (To read the data or Json files and convert Json format)
- PIL - (To Insert and Use Image)
- Easyocr - (To Create and Understand data in computer vision)(Optical Character Recognition)
- cv2 - (To created the binding generators)
- re -  (To use text processing)
- Pandas - (To Clean and manipulate the data)
- Numpy - (To use array and statistical value)
- Time - (To use Time)
# Problem_solution:
### what i did for project solution:
## workflow:
#### Step 1 :
- Python environment (Python 3.x recommended) Streamlit, Pandas, easyOCR, PIL, cv2, matplotlib, re, Psycopg2 libraries installed postgresql server setup and running Features **Home**: Displays an overview of the app including technologies used and a brief description of the app. 
#### Step 2 :
- **Upload & Extract**: This section allows the user to upload an image of a business card. The application then processes the image and extracts data such as company name, card holder name, designation, mobile number, email, website, area, city, state, pin code, and the image of the card.
#### Step 3 : 
- **Modify**: This section allows users to select an entry from the database using a dropdown menu, which they can then update or **delete**. Note: Ensure your PostgreSQL server is running and the database details in the script match your PostgreSQL setup.
#### Step 4 : 
- **About** :This section allows users to knows as the project description and workflows.
## Importing required libraries
### Import Data Handling libraries
```python
import pandas as pd
import numpy as np
```
### Import Text processing 
``` python import easyocr
import cv2
import re    #text processing
```
### Import Dashboard libraries
```python
import streamlit as st
from PIL import Image
from streamlit_option_menu import option_menu
from streamlit_lottie import st_lottie
```
### Import Clone libraries
```python
import requests
import json
```
### if the module shows any error or module not found it can be overcome by using below command
```python
pip install<module name>
```
# E T L Process
## a) Extract data
* Initially, we extract the data from business card by using CV2 and EasyOCR.
- Inorder to fetch the data into to use below code
```python
reader=easyocr.Reader(['en'])
results = reader.readtext(image)
for i in results:
    st.write(f"###### {i[1]}")
```
- Inorder to text extraction bounding image and thresholding
```python
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
new, binary = cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY)
```
## b) Process and Transform the data
### Fetch data
- Extract the data using the code below  
```python
#Website
url_pattern = r"www\.[A-Za-z0-9]+\.[A-Za-z]{2,3}"
url = re.findall(url_pattern, card)
URL = ''
for web in url:
    URL = URL + web
    card = card.replace(web, '')
```
- Extract the other data using like this code
## c) Load  data
### Create Table and Insert into Postgresql
- After insert the dataframe into sql  inner server by using postgresql
- To Establish the connection with sql server
- below table to reference another tables 
```python
#postgresql connect
cont=psycopg2.connect(host='localhost',user='postgres',password='basith',port=5432,database='basith')
csr=cont.cursor()
```
```python
#create tables
csr.execute("""CREATE TABLE if not exists biz_card_data (
                 id SERIAL PRIMARY KEY,
                 name VARCHAR(255),
                 designation VARCHAR(255),
                 company VARCHAR(255),
                 contact VARCHAR(255),
                 email VARCHAR(255),
                 website VARCHAR(255),
                 address VARCHAR(255),
                 city VARCHAR(255),
                 state VARCHAR(255),
                 pincode VARCHAR(255),
                 image bytea )""")
cont.commit()
```
```python
sql = """INSERT INTO biz_card_data (name,designation,company,contact,email,website,address,city,state,pincode,image) 
                                                VALUES (%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)"""
val = (name,designation,company,Phone,Email_id,URL,Address,city,state,Pincode,file_bytes)
csr.execute(sql, val)
cont.commit()
```
# E D A Process 

## a) Access PostgreSQL DB to Modify 

* Create a connection to the postgreSQL server and access the specified postgreSQL DataBase by using **psycopg2** library
```python
selection = st.selectbox("Select specific column to update", column_names)
new_data = st.text_input(f"Enter the new {selection}")
# Define the SQL query to update the selected rows
sql = f"UPDATE biz_card_data SET {selection} = %s WHERE name = %s AND designation = %s"
# Execute the query with the new values
if st.button("Update"):
    csr.execute(sql, (new_data, selection_name, selection_designation))
    # Commit the changes to the database
    cont.commit()
    st.success("updated successfully",icon="👆")
```
## b) Deleting the data
```python
selection_name = st.selectbox("Select name to delete", row_name)
if st.button('DELETE'):
    sql = "DELETE FROM biz_card_data WHERE name = %s AND designation = %s"
# Execute the query with the values as a tuple
    csr.execute(sql, (selection_name, selection_designation))
    cont.commit()
    st.success('###### Deleted successfully',icon='✅')
```
- create the streamlit app with basic tabs [Reference](https://docs.streamlit.io/library/api-reference)
- visualizing the data in streamlit
- streamlit run <filename.py> to run terminal
# Conclusion
- in this project to easly find and extract the data in business cards
- I Created the project to used to detecting the data from business card.
- It mostly used to create the business enviroment and business partner (information) and other uses, store to our database this business card  information
- Easy to see the all business card information and details and edit phone number, mail Id, and other details and delete unnecessary details.

## Outputs and Streamlit UI
- ### Home - page:
![Outlook](https://github.com/mohamedbasith30122001/BizCardX-Extracting-Business-Card-Data-with-OCR/blob/main/bizcard_project_github/output_pages/biz_home.png)
- ### Upload - page:
![Outlook](https://github.com/mohamedbasith30122001/BizCardX-Extracting-Business-Card-Data-with-OCR/blob/main/bizcard_project_github/output_pages/biz_upload_extract.png)
- ### Modify - page:
![Outlook](https://github.com/mohamedbasith30122001/BizCardX-Extracting-Business-Card-Data-with-OCR/blob/main/bizcard_project_github/output_pages/biz_modify.png)
- ### Delete - page:
  ![Outlook](https://github.com/mohamedbasith30122001/BizCardX-Extracting-Business-Card-Data-with-OCR/blob/main/bizcard_project_github/output_pages/biz_delete.png)
 - ### About - page:
![Outlook](https://github.com/mohamedbasith30122001/BizCardX-Extracting-Business-Card-Data-with-OCR/blob/main/bizcard_project_github/output_pages/biz_about.png)


    
