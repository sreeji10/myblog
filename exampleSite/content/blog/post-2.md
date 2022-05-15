---
title: "Creating a CockroachDB cluster"
description: "meta description"
image: "images/post/cockroachdb.png"
date: 2022-05-15T18:19:25+06:00
categories: ["Database"]
type: "featured" # available types: [featured/regular]
draft: false
---

CockroachDB is a distributed SQL database management system, developed by Cockroach Labs. It is relatively new entrant to the database space & designed for speed, scale, and survival. It scales horizontally; survives disk, machine, rack, and even datacenter failures. Likewise, it supports strongly-consistent ACID transactions and provides a familiar SQL API for manipulating and querying data <br> 
If you are building demo machine learning apps then chances are that you need to log/store some training runs or other data. 
Also, if you need to test some API end points for highly distributed application, then you might find CockroachDB Serverless setup much useful.


##### Here is why should definitely check out CockroachDB
The main reason to try out CockroachDB is that they offer a Fully-managed, auto-scale CockroachDB cluster; which you can use to experiment with.

Highlights of the free tier are:
- 5 GB data storage
- 250M Request Units/month
- No credit card required

##### Create your account
-Visit https://cockroachlabs.cloud/signup to create your account </br>
-Enter Email ID, your username & password.</br>
-Credit card & payment setup is not required for the free tier.</br>

<div class="box1" >
{{< image src="images/post/post-2-signup.png" alt="alter-text"  >}}
</div>

##### Create a new cluster
Once you have created your account, it's time to spin up a new database cluster. </br>
-on the login page, click "create cluster" button </br>
-Choose the Serverless plan. </br>
-You can choose either Google Cloud or AWS. </br>
-Choose the region that you would prefer your db server to be hoisted at. </br>
-Edit the cluster name or go with the default one. </br>
-Once your cluster is created, generate and save a password.</br>

<div class="box1" >
{{< image src="images/post/post-2-create_cluster.png" alt="alter-text"  >}}
</div>

##### Create SQL user
Once the cluster is ready, we have to create a SQL user, using which we will interact with the database. </br>
-Define your SQL user ID</br>
-Generate a password. </br>
-Make sure you copy the generated password immediately and save it separately for future use. </br>
-Password will not be displayed again & hence if you save it separately, or else you might have to generate it again.</br>
-Choose the region that you would prefer your db server to be hoisted at. </br>
-Edit the cluster name or go with the default one. </br>
-Once your cluster is created, generate and save a password.</br>

<div class="box">
{{< image  src="images/post/post-2-create_sqluser.png" alt="alter-text" >}}
</div>


##### Connect to Database using our created user ID
-To connect to our Database, we can use the connection string parameters.
-We can connect from our local system using CockroachDB client.
-We can connect using psycopg2, SQLAlchemy etc. if we are using python.

 
<div class="box">
{{< image  src="images/post/post-2-connect.png" alt="alter-text" >}}
</div>

</br>
<hr style="height:2px;border-width:0;color:black;background-color:black">

Thank you for reading this post. </br>
If you want to find how to setup to CockroachDB client in your local system then be sure to check this post [here](http://localhost:1313/blog/post-3/).



<style>
.box1 { 
    background: lightgrey;
    color: black;
    border: 2px solid black;
    margin: 0px auto;

    padding: 2px;
    height: 100%;
    border-radius: 2px;
}
 </style>

<style>
.box { 
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