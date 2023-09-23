
## Data migration from MongoDB into MySQL

In this small project, a SQL database is created based on the data extracted from the NoSQL database (MongoDB). The steps are detailed in the following and the code is presented here <a href="https://github.com/DanialArab/NoSQL/blob/main/Data_Migration_from_MongoDB_to_MySQL/migration.ipynb">Migration - Jupyter Notebook</a>


I first created a NoSQL database named **customers** which has a collection named **information**, as shown in the screenshot below from the MongoDB Compass:

![](https://github.com/DanialArab/images/blob/main/NoSQL/NoSQL_data_in_compass.PNG)

Then I defined SQL schema, extract the data from MongoDB and insert them into the table named consistently as **information** in MySQL:


![](https://github.com/DanialArab/images/blob/main/NoSQL/SQL_table.PNG)
