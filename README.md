# BizCardX-Extracting-Business-Card-Data-with-OCR
## BizCardX: Extracting Business Card Data with OCR using technologies OCR,streamlit GUI, SQL,Data Extraction with Python
# Introduction:
- BizCardX: Extracting Business Card Data with OCR Overview BizCardX is a Streamlit web application which extracts data from business cards using Optical Character Recognition (OCR). Users can upload an image of a business card and the application uses the easyOCR library to extract relevant information from the card. The extracted information is then displayed in a user-friendly format and can be stored in a PostgreSql database for future reference.
## Problem statement:
- developing a Streamlit application that allows users to upload an image of a business card and extract relevant information from it using
easyOCR. The extracted information should include the company name, card holdername, designation, mobile number, email address, website URL, area, city, state,and pin code. The extracted information should then be displayed in the application's graphical user interface (GUI).
In addition, the application should allow users to save the extracted information intoa database along with the uploaded business card image. The database should be able to store multiple entries, each with its own business card image and extracted information.

- Techonlgies used:Python, Streamlit, easyOCR, and a database
management system like SQLite or MySQL or PostgreSQL.

- The application should have a simple and intuitive user interface that guides users through the process of uploading the business card image and extracting its information. The extracted information should be displayed in a clean and organized manner, and users should be able to easily add it to the database with the click of a button. And Allow the user to Read the data,Update the data and Allow the user to delete the data through the streamlit UI

- This project will require skills in image processing, OCR, GUI development, and database management. It will also require you to carefully design and plan the application architecture to ensure that it is scalable, maintainable, and extensible.Good documentation and code organization will also be important for this project.

## problem solution:
### what i did for project solution:
Python environment (Python 3.x recommended) Streamlit, Pandas, easyOCR, PIL, cv2, matplotlib, re, Psycopg2 libraries installed postgresql server setup and running Features **Home**: Displays an overview of the app including technologies used and a brief description of the app. **Upload & Extract**: This section allows the user to upload an image of a business card. The application then processes the image and extracts data such as company name, card holder name, designation, mobile number, email, website, area, city, state, pin code, and the image of the card. **Modify**: This section allows users to select an entry from the database using a dropdown menu, which they can then update or **delete**. The changes are committed to the database. How to Run Clone the repository or download the python script. Run the script using the command line: streamlit run bizcard_project.py The application will open in a new tab of your web browser. You can then navigate through the application, upload images of business cards, and view or modify the extracted data. Note: Ensure your PostgreSQL server is running and the database details in the script match your PostgreSQL setup.

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
