# Using Python to access MySQL in Jupyter notebook

## Store secrets

Create a json file to store your credentials. For example, I created *secrets.json* with the following info

```json
{
    "username":"root",
    "password":"mypasswordhere"
}
```

Using the code below, load your secrets.json file and access the credentials. 

```python
import json

with open('secrets.json') as f:
    login=json.load(f)

myUser = login['username']
myPass = login['password']
```

Make sure to include your variables in the connection string

```python
import mysql.connector

cnx = mysql.connector.connect(user=myUser, 
                              password=myPass,
                              host='127.0.0.1',
                              database='sakila')

cursor = cnx.cursor()

query = ("select first_name, last_name from actor")

cursor.execute(query)

for (first_name, last_name) in cursor:
    print("{} {}".format(first_name, last_name))

cursor.close()
cnx.close()
```
