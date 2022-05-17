---
title: "Connecting to CockroachDB cluster from Python"
description: "connecting to CockroachDB cluster"
image: "images/post/post-4-db.jpeg"
date: 2022-05-16T18:19:25+06:00
categories: ["Database"]
type: "regular" # available types: [featured/regular]
draft: false
---

Here we will connect to CockroachDB database using Python. </br>
Specifically we will be using psycopg2 library</br>



##### Create a Virtual Environment and install psycopg2 library
```console
$ python3 -m venv env
$ source env/bin/activate
(env) $ pip3 install psycopg2-binary

Collecting psycopg2-binary
  Using cached psycopg2_binary-2.9.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.0 MB)
Installing collected packages: psycopg2-binary
Successfully installed psycopg2-binary-2.9.3

```
</br> 

##### Getting the database connection parameters
-To get the connection details, go the cluster details page & take the parameters.

<div class="box1" >
{{< image src="images/post/post-4-connection-dtls.png" alt="alter-text" >}}
</div>
</br>


##### Connect to Database and Create a new table
-here the database name is "defaultdb". 
```python
import psycopg2

conn = psycopg2.connect(
    dbname="tester-1760.defaultdb",
    user="user01",
    password="L-fGdxFbgqQ6srSrYIqRxw",
    host="free-tier8.aws-ap-southeast-1.cockroachlabs.cloud",
    port="26257",
    options="--cluster=tester-1760"
    )

cursor = conn.cursor()
cursor.execute("CREATE TABLE IF NOT EXISTS STUDENT (ID INT PRIMARY KEY, NAME STRING)")
cursor.close()
conn.close()
```

###### Insert data
```python
import psycopg2
conn = psycopg2.connect(
    dbname="tester-1760.defaultdb",
    user="user01",
    password="L-fGdxFbgqQ6srSrYIqRxw",
    host="free-tier8.aws-ap-southeast-1.cockroachlabs.cloud",
    port="26257",
    options="--cluster=tester-1760"
    )

cursor = conn.cursor()
cursor.execute("INSERT INTO STUDENT (ID, NAME) VALUES (1, 'John Doe')")
cursor.close()
conn.close()
```

###### Query data from table
```python
import psycopg2
conn = psycopg2.connect(
    dbname="tester-1760.defaultdb",
    user="user01",
    password="L-fGdxFbgqQ6srSrYIqRxw",
    host="free-tier8.aws-ap-southeast-1.cockroachlabs.cloud",
    port="26257",
    options="--cluster=tester-1760"
    )

cursor = conn.cursor()
cursor.execute("SELECT * FROM STUDENT")
rows = cursor.fetchall()
```
```console
>>> print(rows)
[(1, 'JOHN DOE')]

```


</br>
<hr style="height:2px;border-width:0;color:black;background-color:black">



<style>
.box1 { 
    background: lightgrey;
    color: black;
    border: 2px solid black;
    margin: 0px auto;
    width: 456px;
    padding: 2px;
    height: 100%;
    border-radius: 2px;
}
 </style>