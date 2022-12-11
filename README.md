# Connecting-MySQL-Database-to-Jupyter-Notebook IBM Course

## Objectives
After completing this lab you will be able to:

1. Import the Jupyter Notebook library
2. Enter the database connection credentials
3. Create the database connection
4. Close the database connection


#install the connector library

!%pip install mysql-connector-python


#import the connector
import mysql.connector

#create the connection object and cursor object
from mysql.connector import Error


connection = mysql.connector.connect(host='HOSTNAME',
                                         database='DBNAME',
                                         user='USERNAME',
                                     password='PASSWORD')
if connection.is_connected():
        db_Info = connection.get_server_info()
        print("Connected to MySQL Server version ", db_Info)
        cursor = connection.cursor()
        cursor.execute("select database();")
        record = cursor.fetchone()
        print("You're connected to database: ", record)

else: 
    print("Error while connecting to MySQL", e)


#Construct the Create Table DDL statement 
createQuery = "create table INSTRUCTOR(ID INTEGER PRIMARY KEY NOT NULL, FNAME VARCHAR(20), LNAME VARCHAR(20), CITY VARCHAR(20), CODE CHAR(2))"

#Now fill in the name of the method and execute the statement
createStmt = cursor.execute(createQuery)


#Construct the query 
insertQuery = "insert into INSTRUCTOR values (1, 'Rav', 'Ahuja', 'TORONTO', 'CA')"
selectQuery = "select * from INSTRUCTOR"


#execute the insert statement
insertStmt = cursor.execute(insertQuery)
connection.commit()
selectStmt = cursor.execute(selectQuery)
cursor.fetchall()


#replace ... with the insert statement that inerts the remaining two rows of data
insertQuery2 = "insert into INSTRUCTOR values (2, 'Raul', 'Chong', 'Markham', 'CA'), (3, 'Hima', 'Vasudevan', 'Chicago', 'US')"

#execute the statement
insertStmt2 = cursor.execute(insertQuery2)
connection.commit()
selectStmt = cursor.execute(selectQuery)
cursor.fetchall()


#Enter your code below
updateQuery = "update INSTRUCTOR set CITY='MOOSETOWN' where FNAME='Rav'"
updateStmt = cursor.execute(updateQuery)
connection.commit()


#Construct the query that retrieves all rows from the INSTRUCTOR table
selectQuery = "select * from INSTRUCTOR"

#Execute the statement
selectStmt = cursor.execute(selectQuery)


#Fetch the Dictionary (for the first row only) - replace ... with your code
cursor.fetchall()


import pandas

pdf = pandas.read_sql(selectQuery, connection)
pdf


pdf.shape


cursor.close()
connection.close()
print("MySQL connection is closed")
