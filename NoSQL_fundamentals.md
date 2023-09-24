# NoSQL

Reference: <a href="https://www.udemy.com/course/introduction-to-mongodb/?utm_source=adwords-learn&utm_medium=udemyads&utm_campaign=DSA_CA_Tech&utm_content=deal4584&utm_term=_._ag_76808851565_._ad_533102607579_._de_c_._dm__._pl__._ti_dsa-796176360685_._li_9001497_._pd__._&gclid=Cj0KCQjw06-oBhC6ARIsAGuzdw0YatK9S42zHe7Ml6tPW_MBmrBcWXUeE-W43oxmwKPiGX_L3Qq5EJ8aApJPEALw_wcB">Introduction to MongoDB for Data Analytics  </a>

1. [Introduction](#1)
   1. [SQL vs. NoSQL](#2)
      1. [Schema](#3)
      2. [Flexibility](#4)
      3. [Transactional systems](#5)
      4. [Vertical vs. Horizontal scaling](#6)
      5. [CRUD](#7)
2. [Getting started with databases - Practical](#8)
   1. [Starting a MongoDB server and shelll](#9)
   2. [Creating a database/collection](#10)
   3. [Inserting documents (adding data to the collections)](#11)
   4. [Intro to queries using find](#12)
   5. [Updating documents](#13)
   6. [Deleting documents](#14)
3. [Database design - intuition](#15)
   1. [Primary keys](#16)
   2. [Establishing relationships in data](#17)
   3. [Embeded documents](#18)
   4. [Embeded documents vs. separate collections](#19)
4. [Database design - practical](#20)
5. [Data analysis - intuition](#21)
   1. [Quantitative vs. categorical data](#22)



<a name="1"></a>
## Introduction

<a name="2"></a>
### SQL vs. NoSQL

NoSQL = Not only SQL

![](https://github.com/DanialArab/images/blob/main/NoSQL/sql%20vs%20nosql%200.PNG)

![](https://github.com/DanialArab/images/blob/main/NoSQL/sql%20vs%20nosql%202.PNG)

<a name="3"></a>
#### Schema

+ **Schema is a mapping of the structure of your data**. It will tell you how many columns you'll have in a table for example what type of data each column will store and things like that
  In SQL, The schema is **predetermined** when your database is created. And so changing your schema after the fact is very difficult. And one thing that this means is that you need to do a bunch of **prep work upfront to define the exact schema that you will**. And this won't necessarily be the case with no sequel because it no sequel your schema is not predefined.
+ So in our sequel example one of the blog posts has no dislikes and then the other has no likes in sequel because **all of our data has to have the same structure**, each of these posts would have to have a likes field and a dislikes field but because in **no sequel our schema is flexible**, We don't have to have the same exact keys and values for every document. We could just not include a dislikes field for the post that doesn't have any dislikes. And then we could also leave out the likes field for this post that has no likes

<a name="4"></a>
#### Flexibility

+ In a SQL table each row in that table needs to have the same columns/attributes as all the other rows in the table. **But you can't have one row have an extra column that another row does not have while in MongoDB each collection can have documents that have different structures not every document in a collection has to have the same keys or the same number of keys as another.**
+ In MongoDB, we can do something very interesting. We can combine our post and the comments that go with a blog post into a single document. And this means that rather than needing to have separate tables or in the case of Mongo D.B. separate collections for posts and their comments we can have a single collection that stores everything:
  
![](https://github.com/DanialArab/images/blob/main/NoSQL/sql.PNG)

![](https://github.com/DanialArab/images/blob/main/NoSQL/nosql.PNG)

<a name="5"></a>
#### Transactional systems 

![](https://github.com/DanialArab/images/blob/main/NoSQL/sql%20vs%20nosql%203.PNG)

+ A transaction is essentially when multiple database operations need to be completed in order for a single action to take place.
+ Let's say that when we initiate the transaction we end up successfully completing two of the operations. So we add a row to our transactions table and we subtract the amount from Marie's account balance. But there's a problem when adding the amount to Robert's account balance maybe there is a power outage for the server's power supply where these databases are being hosted or a program crashed in the process or something like that. If we weren't prepared to handle this that would definitely be a bad situation because Marie would see that she had lost money and there'd be a record of the transaction occurring. But Robert never would have received the money and so he would be confused and probably angry about that happening. In general, **relational databases are built to handle this problem so that none of the database operations will go through if a single operation in the transaction cannot be performed**

<a name="6"></a>
#### Vertical vs. Horizontal scaling

+ **Vertical scaling** is when you increase the storage capacity of individual database servers that you are currently using. And this could mean adding more RAM. It could be increasing the processing power of the CPSU or things like that.
+ **Horizontal scaling** on the other hand is when you add **more servers to your database cluster.** So rather than having to modify the existing servers you're using you could just add more of them every time you need to scale up or every time you need more storage space.
+ Generally speaking, sequel databases can scale vertically but are more difficult to scale horizontally while no sequel databases are generally much easier to scale horizontally.
+ It's generally **more expensive to upgrade the hardware on a single server than it would be to just add more and more low-cost servers every time you need to scale**, which makes **horizontal scaling, in general, a more cost-effective and advantageous approach** if it works for the data structures that we are using. This plays into why MongoDB and other no sequel databases are becoming **very popular for handling big data and large-scale database needs**.
+ **In NoSQL, we have the posts and comments in a single document grouped together allowing us to access them in one server, while in SQL database, we may have our tables like posts and comments tables in various servers. And if that were the case we would need to make network requests between those servers when pulling a blog post and its comments at the same time. And this is much less efficient than pulling a single document from a single server where you don't need to communicate between servers for the same operation. You can get it all from one place. And in addition to being less efficient, it also can cause other problems and complications.**

<a name="7"></a>
#### CRUD

**CRUD = CREATE READ UPDATE DELETE**

Four primary database operations that every database programmer uses to interact with the database.
+ create is when you insert one or more records into your database
+ read is when you pull records from the database either to display in a user interface for analysts or to poll to display on a web page or something like that.
+ Update is when you modify records that already exist in the database and
+ delete is when you remove records from the database

      CREATE: db.collection.insert({'name' : 'Danial'})
      READ: db.collection.find({'age': 24}) 
      UPDATE db.collection.update({'country': 'US'}, {'country': 'USA'}) 
      DELETE: db.collection.remove({'user_id', 1024})


<a name="8"></a>
##  Getting started with databases - Practical

<a name="9"></a>
### Starting a MongoDB server and shell

First I need to start up a MongoDB server and shell:

I start up a MongoDB server in the command prompt by copying and pasting the following command:

      "C:\Program Files\MongoDB\Server\7.0\bin\mongod.exe" --dbpath="c:\data\db"

Then I need to have another cmd prompt to start up a MongoDB shell. In my version, there was no mongo.exe and so I needed to download the 'mongosh-1.10.6-win32-x64' from the net that contains mongosh.exe. I need to copy and paste the following in the cmd prompt: 

      "D:\0_Machine_Learning\Software -- ML Journey\22. MongoDB\mongosh-1.10.6-win32-x64\bin\mongosh.exe"
   
<a name="10"></a>
### Creating a database/collection

to see the databases

      show dbs

returns

      admin    40.00 KiB
      config  108.00 KiB
      local    72.00 KiB

      
to create a database named test and switch to it:

      use test
      
so the database test is the active database meaning the one that we are using right now. 

Also, the same command can be used to switch between the existing databases like 

      use admin

#### collection

In MongoDB, within a database there are collections and **a collection is essentially a group of data kind of similar to a table in SQL.**

To create a collection we use a createCollection method:

      db.createCollection('name_of_my_collection') 

like

      test> db.createCollection('users')

returns back 

      { ok: 1 }

meaning the collection creation was successful. We can validate it through

      show collections

returns back

      test> show collections
      users

<a name="11"></a>
### Inserting documents (adding data to the collections)


      test> db.users.insert({'name': 'James'})
      {
        acknowledged: true,
        insertedIds: { '0': ObjectId("650db967e0557b6b3a8824a1") }
      }
      
      
      test> db.users.insert({'name': 'Julia', 'age': 24})
      {
        acknowledged: true,
        insertedIds: { '0': ObjectId("650db98de0557b6b3a8824a2") }
      }
     

<a name="12"></a>
### Intro to queries using find

      test> db.users.find()
      [
        { _id: ObjectId("650db967e0557b6b3a8824a1"), name: 'James' },
        { _id: ObjectId("650db98de0557b6b3a8824a2"), name: 'Julia', age: 24 },
        {
          _id: ObjectId("650dba44e0557b6b3a8824a3"),
          name: 'Daniel',
          age: 28
        },
        { _id: ObjectId("650dba63e0557b6b3a8824a4"), name: 'Jim', age: 36 }
      ]
 
There is this additional key-value pair over here called **_id** and then we have this object id and then a string of characters, this is something that **MongoDB adds to every document you insert into a collection by default. And the reason that it does this is so that every document will have some unique key or a key that has a value that is unique to that document.** So let's say for example if we had created two users with the same name like two users with the name of James this object id would be something that we could use to uniquely identify this document even if all of the other key-value pairs were identical to another document for example.

      test> db.users.find({'name': 'Jim'})
      [
        { _id: ObjectId("650dba63e0557b6b3a8824a4"), name: 'Jim', age: 36 }
      ]

or

      test> db.users.insert({'name': 'Mo', 'age': 36})
      {
        acknowledged: true,
        insertedIds: { '0': ObjectId("650dbbe4e0557b6b3a8824a5") }
      }
      test> db.users.find({'age': 36})
      [
        { _id: ObjectId("650dba63e0557b6b3a8824a4"), name: 'Jim', age: 36 },
        { _id: ObjectId("650dbbe4e0557b6b3a8824a5"), name: 'Mo', age: 36 }
      ]

To query for fields that have missing values:

      test> db.users.find({"age": null})
      [ { _id: ObjectId("650db967e0557b6b3a8824a1"), name: 'James' } ]

To grab users who were all a certain age or older (gt below means greater than):

      test> db.users.find({"age": {$gt: 22}})
      [
        { _id: ObjectId("650db98de0557b6b3a8824a2"), name: 'Julia', age: 24 },
        {
          _id: ObjectId("650dba44e0557b6b3a8824a3"),
          name: 'Daniel',
          age: 28
        },
        { _id: ObjectId("650dba63e0557b6b3a8824a4"), name: 'Jim', age: 36 },
        { _id: ObjectId("650dbbe4e0557b6b3a8824a5"), name: 'Mo', age: 36 }
      ]

for less than a value (lt means less than in below):

      test> db.users.find({"age": {$lt: 30}})
      [
        { _id: ObjectId("650db98de0557b6b3a8824a2"), name: 'Julia', age: 24 }
      ]

<a name="13"></a>
### Updating documents

      test> db.users.update({'name': 'James'}, {$set: {'name': 'James', 'age': 22}})
      {
        acknowledged: true,
        insertedId: null,
        matchedCount: 1,
        modifiedCount: 0,
        upsertedCount: 0
      }

      test> db.users.find( )
      [
        { _id: ObjectId("650db967e0557b6b3a8824a1"), name: 'James', age: 22 },
        { _id: ObjectId("650db98de0557b6b3a8824a2"), name: 'Julia', age: 24 },
        {
          _id: ObjectId("650dba44e0557b6b3a8824a3"),
          name: 'Daniel',
          age: 28
        },
        { _id: ObjectId("650dba63e0557b6b3a8824a4"), name: 'Jim', age: 36 },
        { _id: ObjectId("650dbbe4e0557b6b3a8824a5"), name: 'Mo', age: 36 }
      ]



<a name="14"></a>
### Deleting documents


      test> db.users.find()
      [
        { _id: ObjectId("650db967e0557b6b3a8824a1"), name: 'James', age: 22 },
        { _id: ObjectId("650db98de0557b6b3a8824a2"), name: 'Julia', age: 24 },
        {
          _id: ObjectId("650dba44e0557b6b3a8824a3"),
          name: 'Daniel',
          age: 28
        },
        { _id: ObjectId("650dba63e0557b6b3a8824a4"), name: 'Jim', age: 36 },
        { _id: ObjectId("650dbbe4e0557b6b3a8824a5"), name: 'Mo', age: 36 }
      ]
      
      test> db.users.remove({'name': 'James'})
      { acknowledged: true, deletedCount: 1 }
      test> db.users.find()
      [
        { _id: ObjectId("650db98de0557b6b3a8824a2"), name: 'Julia', age: 24 },
        {
          _id: ObjectId("650dba44e0557b6b3a8824a3"),
          name: 'Daniel',
          age: 28
        },
        { _id: ObjectId("650dba63e0557b6b3a8824a4"), name: 'Jim', age: 36 },
        { _id: ObjectId("650dbbe4e0557b6b3a8824a5"), name: 'Mo', age: 36 }
      ]
      


<a name="15"></a>
## Database design - intuition
  
<a name="16"></a>
### Primary keys

Primary keys have a larger role in sequel databases than they do in no sequel. But they still do make an appearance in MongoDB. 

+ They are unique for all documents in a collection
+ cannot have null values

So in MongoDB whenever a new document is created this **_id** key is automatically added to it:

![](https://github.com/DanialArab/images/blob/main/NoSQL/pkey.PNG) 

The default value for _id is an object id data type which is a special data type in MongoDB. That's not any of the ones that we have gone over so far like string integer float or boolean and inside this data type there is this long hexadecimal string that is always unique for each document in a collection and this is built into the structure of MongoDB to ensure that each document has this _id key that it has a no null value or a non-missing value and that all documents within the same collection will have a unique value for this _id property.

Even though each document will have this _id primary key and that will always be unique for each document by default it's often beneficial to define another unique identifier for records in a collection:

![](https://github.com/DanialArab/images/blob/main/NoSQL/pkey2.PNG)

It's more human readable and also an integer as a data type. Here for this unique identifier can sometimes be easier to work with in your programs and analysis than this object I.D. that Mongo uses. And also you might want to have an I.D. that increases sequentially each time a new record is added. While Mongo D.B. enforces uniqueness on this underscore I.D. key by default you could also build it into the structure of your database to enforce uniqueness on this user I.D. key as well. Or a developer could potentially build this in at the application level. So for example when a new user creates an account a unique I.D. would have been chosen for that user before anything even gets into the database.

<a name="17"></a>
### Establishing relationships in data

**Even though MongoDB and no SQL databases are known as non-relational databases it can still be beneficial to establish relationships between different documents and different collections.**:

![](https://github.com/DanialArab/images/blob/main/NoSQL/relationships%20in%20data.PNG)

A one-to-one relationship is where each document relates to exactly one other document. And this could be either in the same collection or in a separate collection a one to many relationship is where one document can relate to many other documents but each of those documents can only relate to the original document. And a Many to Many relationship is where each document can relate to many other documents. But each of those can also relate to many other documents.

![](https://github.com/DanialArab/images/blob/main/NoSQL/one%20to%20one.PNG)

![](https://github.com/DanialArab/images/blob/main/NoSQL/one%20to%20many.PNG)

"![](https://github.com/DanialArab/images/blob/main/NoSQL/many%20to%20many.PNG)

<a name="18"></a>
### Embedded documents

Embedded documents can be a particularly helpful way to establish a one-to-many relationship in MongoDB. 

![](https://github.com/DanialArab/images/blob/main/NoSQL/embedded%20doc.PNG)

Each of our blog posts no longer has the default underscore I.D. key or the Post's I.D. key. And we actually don't need these anymore, when we're using embedded documents because for the posts key we have a list (which is, of course, zero-indexed) as values. So even though each post doesn't have a primary key within this embedded document it corresponds to a unique index in the Post's array. So we can still uniquely identify each post for a given user. 

<a name="19"></a>
### Embedded documents vs. separate collections

We should think about which one might be more beneficial. And the answer really depends on the particular use case but in general for each situation in which you are reading data from your database so in which your data is being accessed either to display on a Web site for users or to be pulled in queries for analysis in each one of those situations your goals should be to **minimize the amount of data that is unnecessarily loaded and to access all of the data that you will need in one single query ideally or in the minimum number of queries possible.**

<a name="20"></a>
## Database design - practical

MongoDB Compass is a **graphical user interface (GUI) for MongoDB**, designed to help developers and database administrators interact with MongoDB databases more easily. It provides a visual way to explore and manipulate data, manage databases, and perform various tasks related to MongoDB. We're going to install a tool called MongoDB compass that's going to help us visualize data more effectively and we'll actually not require us to continue using the shell. And while I thought it was a really good learning opportunity to execute commands in the shell and work with the raw data format of MongoDB going forward as we deal with designing databases and analyzing data it's gonna be really helpful to visualize our data in a more efficient way. And that's something that MongoDB compass is going to help us do. 

**We need to have MongoDB server running to be able to make the operations in Compass.**

My test database and users collection in MongoDB Compass:

![](https://github.com/DanialArab/images/blob/main/NoSQL/compass.PNG)

+ Compass allows us to perform CRUD using the GUI.
+ So if we hover over a document and then over to the right hand side and click on **clone document** that will open up the user record and we can just change the values rather than having to type out each key over again we can just change the values to represent our new user.
+ Rather than working with GUI in Compass, we use the Mongo Shell to add multiple posts into our posts collection at the same time so that we an have more data to work with without having to enter it all in manually: 

So to get started with that you can go to your terminal and if you've been following along with the

      db.posts.insert([
      	{
      		"body": "I’ve been trying out Overnight Oats for breakfast every morning this week. Super easy to make and a great way to start the day!", 
      		"topic": "cooking",
      		"likes": 23,
      		"dislikes": 12,
      		"user_id": 4
      	},
      	{
      		"body": "I went to Hawaii last month and had the best Acai bowl I’ve ever had! Trying to find some good recipes to make my own but haven’t found anything good so far. Anyone have any good recommendations?",
      		"topic": "cooking",
      		"likes": 13,
      		"dislikes": 31,
      		"user_id": 4
      	},
      	{
      		"body": "I’ve been having greek yogurt every morning for breakfast lately - great way to get a good source of protein if you’re looking for good vegetarian-friendly options.",
      		"topic": "cooking",
      		"likes": 21,
      		"dislikes": 26,
      		"user_id": 1
      	},
      	{
      		"body": "I’ve been running four days per week for the last three weeks. Definitely a struggle, but last week I ran an hour for each workout while previously I was running 45 minutes per workout. Making progress!",
      		"topic": "fitness",
      		"likes": 57,
      		"dislikes": 33,
      		"user_id": 2
      	},
      	{
      		"body": "I started taking this yoga class about two months ago. It’s done wonders for my posture and also has helped strengthen my core a great deal. Definitely recommend it.",
      		"topic": "fitness",
      		"likes": 42,
      		"dislikes": 11,
      		"user_id": 3
      	},
      	{
      		"body": "I was doing squats at the gym yesterday and I think I may have pulled a hamstring. After I take some time to rest, I’ll need to focus on my form and make sure to not to add more weight than I’m comfortable with.",
      		"topic": "fitness",
      		"likes": 28,
      		"dislikes": 37,
      		"user_id": 3
      	},
      	{
      		"body": "Just went surfing in Half Moon Bay. The waves have been pretty awesome all week but be careful. Definitely not for beginners and it’s really cold out there - don’t forget to bring a wetsuit!",
      		"topic": "sports",
      		"likes": 41,
      		"dislikes": 17,
      		"user_id": 5
      	},
      	{
      		"body": "I just tried out the clip-in bike pedals on my road bike. They’re awesome! I’m already noticing that my performance increasing compared to my other rides this week. Definitely recommend them if you’re a cyclist and haven’t tried it!",
      		"topic": "sports",
      		"likes": 38,
      		"dislikes": 33,
      		"user_id": 5
      	},
      	{
      		"body": "I was playing basketball today after work and I made a half-court shot for the first time! Definitely a lot of luck involved, but still a big win!",
      		"topic": "sports",
      		"likes": 26,
      		"dislikes": 19,
      		"user_id": 2
      	}
      
      ])

Creating an embedded document in Compass:

![](https://github.com/DanialArab/images/blob/main/NoSQL/embedded%20duc%202.PNG)

When building or designing a database we need to ask: how can I structure it so that for the particular analysis that I'm making I will be able to get all of the information I need with the smallest number of queries possible without loading data that's unnecessary for my given use case.

<a name="21"></a>
## Data analysis - intuition

<a name="22"></a>
### Quantitative vs. categorical data

