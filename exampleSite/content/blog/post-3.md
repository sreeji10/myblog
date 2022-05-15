---
title: "Installing CockroachDB client on Ubuntu 20.04"
description: "meta description"
image: "images/post/cockroachdb.png"
date: 2022-05-15T18:19:25+06:00
categories: ["Database"]
type: "featured" # available types: [featured/regular]
draft: false
---

Here we will install the CockroachDB database & client on Ubuntu 20.04 Operating system </br>
You will need to use sudo if you get any permission errors. </br>



##### Download CockroachDB libraries
```console
$ curl https://binaries.cockroachdb.com/cockroach-v21.2.10.linux-amd64.tgz | tar -xz && sudo cp -i cockroach-v21.2.10.linux-amd64/cockroach /usr/local/bin/
```


Note: To get started with CockroachDB, we dont need to install the additional GEOS libraries. </br>
Please follow [this](https://www.cockroachlabs.com/docs/v21.2/install-cockroachdb-linux.html)  documentation for setting up GEOS libraries. 

</br> 

##### Downloading CA Certifcate
-Now once the client is installed, we need to download the CA Certificate so that we can connect remotely to the database.</br>
-The command to download the same is OS dependent and same can be found on the custers page.</br>
-Click on the Connect button on the custer webpage and it should open up a popup window.</br>
-Copy the Download CA-Cert command

<div class="box1" >
{{< image src="images/post/post-3_connect.png" alt="alter-text" >}}
</div>
</br>


-Execute the command in the terminal </br>
-This will download the certifate the the logged-in users home directory.

```console
$ curl --create-dirs -o $HOME/.postgresql/root.crt -O https://cockroachlabs.cloud/clusters/7f5acd64-69eb-4684-bd61-d7cdb946a678/cert
```

##### Connecting to Database
-When we create a cluster, by default we will get a Database which is called "defaultdb" </br>
-We can connect to the database using the below Connection string. </br>
-Make sure you pass in the correct path for the "sslrootcert" parameter. </br>
 
```console
cockroach sql --url 'postgresql://user01:L-fGdxFbgqQ6srSrYIqRxw@free-tier8.aws-ap-southeast-1.cockroachlabs.cloud:26257/defaultdb?sslmode=verify-full&sslrootcert='$HOME'/.postgresql/root.crt&options=--cluster=tester-1760'
```

###### After logging-in, below messages will be displayed.
```console
#
# Welcome to the CockroachDB SQL shell.
# All statements must be terminated by a semicolon.
# To exit, type: \q.
#
# Client version: CockroachDB CCL v21.1.19 (x86_64-unknown-linux-gnu, built 2022/05/09 15:01:31, go1.15.14)
# Server version: CockroachDB CCL v21.2.10 (x86_64-unknown-linux-gnu, built 2022/05/02 17:38:58, go1.16.6)
# Cluster ID: 9db6a4da-a8ac-439a-bfd1-3332d059190e
No entry for terminal type "xterm-256color";
using dumb terminal settings.
#
# Enter \? for a brief introduction.
#
user01@free-tier8.aws-ap-southeast-1.cockroachlabs.cloud:26257/defaultdb>
```

##### Creating a table & querying it
```console
user01@free-tier8.aws-ap-southeast-1.cockroachlabs.cloud:26257/defaultdb> create table student (id int, name varchar(30)); 
CREATE TABLE

Time: 90ms total (execution 10ms / network 80ms)


user01@free-tier8.aws-ap-southeast-1.cockroachlabs.cloud:26257/defaultdb> insert into student values (1, 'JOHN DOE');         
INSERT 1

Time: 101ms total (execution 3ms / network 98ms)

user01@free-tier8.aws-ap-southeast-1.cockroachlabs.cloud:26257/defaultdb> select * from student;
  id |   name
-----+-----------
   1 | JOHN DOE
(1 row)

Time: 94ms total (execution 2ms / network 92ms)
```

</br>
<hr style="height:2px;border-width:0;color:black;background-color:black">

Thank you for reading this post. </br>
If you would like to know how to connect to CockroachDB server using Python; then be sure to check this post [here](http://localhost:1313/blog/post-4/).


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