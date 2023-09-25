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
   2. [Analysis techniques](#23)
      1. [Projection](#24)
      2. [Exploration](#25)
   3. [Using the Midpoint for Quantitative Data Exploration](#26)
4. [Data analysis practical- blog case study](#27)
   1. [Exploring the data](#28)
      1. [Sorting](#29)
      2. [Projection](#30)
      3. [Filter](#31)
   2. [Identifying correlations in data](#32)



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

![](https://github.com/DanialArab/images/blob/main/NoSQL/Quantitative%20vs.%20categorical%20data.PNG)

<a name="23"></a>
### Analysis techniques

<a name="24"></a>
#### Projection

We will be using this to only return the fields in the document that we specifically want to work with and our analysis. And for us the main purpose is mainly for readability to make it easier for us to work with data by only focusing on the fields that are important to us. So if we project those fields we can remove the fields that we don't want to work with and only display the fields that we're interested in using projection and the _id Key will always be present in our documents because it is the primary key it's the unique identifier for each individual document. In projection, we don't actually remove any fields from documents in terms of how they're stored. It's not like we actually lost data. It's just returning specific fields in our query that we want to work with.

<a name="25"></a>
#### Exploration

Our goal in this phase will be to learn about how our documents are distributed with respect to each of the attributes that we are focusing on. And we're going to have different approaches for doing this for categorical data versus quantitative data.

<a name="26"></a>
### Using the Midpoint for Quantitative Data Exploration

![](https://github.com/DanialArab/images/blob/main/NoSQL/Exploration.PNG)

<a name="27"></a>
## Data analysis practical- blog case study

      blog_analysis> db.users.stats()
      {
        ok: 1,
        capped: false,
        wiredTiger: {
          metadata: { formatVersion: 1 },
          creationString: 'access_pattern_hint=none,allocation_size=4KB,app_metadata=(formatVersion=1),assert=(commit_timestamp=none,durable_timestamp=none,read_timestamp=none,write_timestamp=on),block_allocation=best,block_compressor=snappy,cache_resident=false,checksum=on,colgroups=,collator=,columns=,dictionary=0,encryption=(keyid=,name=),exclusive=false,extractor=,format=btree,huffman_key=,huffman_value=,ignore_in_memory_cache_size=false,immutable=false,import=(compare_timestamp=oldest_timestamp,enabled=false,file_metadata=,metadata_file=,repair=false),internal_item_max=0,internal_key_max=0,internal_key_truncate=true,internal_page_max=4KB,key_format=q,key_gap=10,leaf_item_max=0,leaf_key_max=0,leaf_page_max=32KB,leaf_value_max=64MB,log=(enabled=true),lsm=(auto_throttle=true,bloom=true,bloom_bit_count=16,bloom_config=,bloom_hash_count=8,bloom_oldest=false,chunk_count_limit=0,chunk_max=5GB,chunk_size=10MB,merge_custom=(prefix=,start_generation=0,suffix=),merge_max=15,merge_min=0),memory_page_image_max=0,memory_page_max=10m,os_cache_dirty_max=0,os_cache_max=0,prefix_compression=false,prefix_compression_min=4,source=,split_deepen_min_child=0,split_deepen_per_child=0,split_pct=90,tiered_storage=(auth_token=,bucket=,bucket_prefix=,cache_directory=,local_retention=300,name=,object_target_size=0),type=file,value_format=u,verbose=[write_timestamp],write_timestamp_usage=none',
          type: 'file',
          uri: 'statistics:table:collection-8-8667477942090323950',
          LSM: {
            'bloom filter false positives': 0,
            'bloom filter hits': 0,
            'bloom filter misses': 0,
            'bloom filter pages evicted from cache': 0,
            'bloom filter pages read into cache': 0,
            'bloom filters in the LSM tree': 0,
            'chunks in the LSM tree': 0,
            'highest merge generation in the LSM tree': 0,
            'queries that could have benefited from a Bloom filter that did not exist': 0,
            'sleep for LSM checkpoint throttle': 0,
            'sleep for LSM merge throttle': 0,
            'total size of bloom filters': 0
          },
          autocommit: {
            'retries for readonly operations': 0,
            'retries for update operations': 0
          },
          'block-manager': {
            'allocations requiring file extension': 4,
            'blocks allocated': 4,
            'blocks freed': 0,
            'checkpoint size': 4096,
            'file allocation unit size': 4096,
            'file bytes available for reuse': 0,
            'file magic number': 120897,
            'file major version number': 1,
            'file size in bytes': 20480,
            'minor version number': 0
          },
          btree: {
            'btree checkpoint generation': 1193,
            'btree clean tree checkpoint expiration time': Long("9223372036854775807"),
            'btree compact pages reviewed': 0,
            'btree compact pages rewritten': 0,
            'btree compact pages skipped': 0,
            'btree skipped by compaction as process would not reduce size': 0,
            'column-store fixed-size leaf pages': 0,
            'column-store fixed-size time windows': 0,
            'column-store internal pages': 0,
            'column-store variable-size RLE encoded values': 0,
            'column-store variable-size deleted values': 0,
            'column-store variable-size leaf pages': 0,
            'fixed-record size': 0,
            'maximum internal page size': 4096,
            'maximum leaf page key size': 2867,
            'maximum leaf page size': 32768,
            'maximum leaf page value size': 67108864,
            'maximum tree depth': 3,
            'number of key/value pairs': 0,
            'overflow pages': 0,
            'row-store empty values': 0,
            'row-store internal pages': 0,
            'row-store leaf pages': 0
          },
          cache: {
            'bytes currently in the cache': 35011,
            'bytes dirty in the cache cumulative': 1272,
            'bytes read into cache': 0,
            'bytes written from cache': 14555,
            'checkpoint blocked page eviction': 0,
            'checkpoint of history store file blocked non-history store page eviction': 0,
            'data source pages selected for eviction unable to be evicted': 0,
            'eviction gave up due to detecting a disk value without a timestamp behind the last update on the chain': 0,
            'eviction gave up due to detecting a tombstone without a timestamp ahead of the selected on disk update': 0,
            'eviction gave up due to detecting a tombstone without a timestamp ahead of the selected on disk update after validating the update chain': 0,
            'eviction gave up due to detecting update chain entries without timestamps after the selected on disk update': 0,
            'eviction gave up due to needing to remove a record from the history store but checkpoint is running': 0,
            'eviction walk passes of a file': 0,
            'eviction walk target pages histogram - 0-9': 0,
            'eviction walk target pages histogram - 10-31': 0,
            'eviction walk target pages histogram - 128 and higher': 0,
            'eviction walk target pages histogram - 32-63': 0,
            'eviction walk target pages histogram - 64-128': 0,
            'eviction walk target pages reduced due to history store cache pressure': 0,
            'eviction walks abandoned': 0,
            'eviction walks gave up because they restarted their walk twice': 0,
            'eviction walks gave up because they saw too many pages and found no candidates': 0,
            'eviction walks gave up because they saw too many pages and found too few candidates': 0,
            'eviction walks reached end of tree': 0,
            'eviction walks restarted': 0,
            'eviction walks started from root of tree': 0,
            'eviction walks started from saved location in tree': 0,
            'hazard pointer blocked page eviction': 0,
            'history store table insert calls': 0,
            'history store table insert calls that returned restart': 0,
            'history store table reads': 0,
            'history store table reads missed': 0,
            'history store table reads requiring squashed modifies': 0,
            'history store table resolved updates without timestamps that lose their durable timestamp': 0,
            'history store table truncation by rollback to stable to remove an unstable update': 0,
            'history store table truncation by rollback to stable to remove an update': 0,
            'history store table truncation to remove all the keys of a btree': 0,
            'history store table truncation to remove an update': 0,
            'history store table truncation to remove range of updates due to an update without a timestamp on data page': 0,
            'history store table truncation to remove range of updates due to key being removed from the data page during reconciliation': 0,
            'history store table truncations that would have happened in non-dryrun mode': 0,
            'history store table truncations to remove an unstable update that would have happened in non-dryrun mode': 0,
            'history store table truncations to remove an update that would have happened in non-dryrun mode': 0,
            'history store table updates without timestamps fixed up by reinserting with the fixed timestamp': 0,
            'history store table writes requiring squashed modifies': 0,
            'in-memory page passed criteria to be split': 0,
            'in-memory page splits': 0,
            'internal page split blocked its eviction': 0,
            'internal pages evicted': 0,
            'internal pages split during eviction': 0,
            'leaf pages split during eviction': 0,
            'modified pages evicted': 0,
            'overflow keys on a multiblock row-store page blocked its eviction': 0,
            'overflow pages read into cache': 0,
            'page split during eviction deepened the tree': 0,
            'page written requiring history store records': 0,
            'pages read into cache': 0,
            'pages read into cache after truncate': 0,
            'pages read into cache after truncate in prepare state': 0,
            'pages requested from the cache': 207,
            'pages seen by eviction walk': 0,
            'pages written from cache': 2,
            'pages written requiring in-memory restoration': 0,
            'recent modification of a page blocked its eviction': 0,
            'reverse splits performed': 0,
            'reverse splits skipped because of VLCS namespace gap restrictions': 0,
            'the number of times full update inserted to history store': 0,
            'the number of times reverse modify inserted to history store': 0,
            'tracked dirty bytes in the cache': 0,
            'uncommitted truncate blocked page eviction': 0,
            'unmodified pages evicted': 0
          },
          cache_walk: {
            'Average difference between current eviction generation when the page was last considered': 0,
            'Average on-disk page image size seen': 0,
            'Average time in cache for pages that have been visited by the eviction server': 0,
            'Average time in cache for pages that have not been visited by the eviction server': 0,
            'Clean pages currently in cache': 0,
            'Current eviction generation': 0,
            'Dirty pages currently in cache': 0,
            'Entries in the root page': 0,
            'Internal pages currently in cache': 0,
            'Leaf pages currently in cache': 0,
            'Maximum difference between current eviction generation when the page was last considered': 0,
            'Maximum page size seen': 0,
            'Minimum on-disk page image size seen': 0,
            'Number of pages never visited by eviction server': 0,
            'On-disk page image sizes smaller than a single allocation unit': 0,
            'Pages created in memory and never written': 0,
            'Pages currently queued for eviction': 0,
            'Pages that could not be queued for eviction': 0,
            'Refs skipped during cache traversal': 0,
            'Size of the root page': 0,
            'Total number of pages currently in cache': 0
          },
          'checkpoint-cleanup': {
            'pages added for eviction': 0,
            'pages removed': 0,
            'pages skipped during tree walk': 0,
            'pages visited': 1
          },
          compression: {
            'compressed page maximum internal page size prior to compression': 4096,
            'compressed page maximum leaf page size prior to compression ': 131072,
            'compressed pages read': 0,
            'compressed pages written': 1,
            'number of blocks with compress ratio greater than 64': 0,
            'number of blocks with compress ratio smaller than 16': 0,
            'number of blocks with compress ratio smaller than 2': 0,
            'number of blocks with compress ratio smaller than 32': 0,
            'number of blocks with compress ratio smaller than 4': 0,
            'number of blocks with compress ratio smaller than 64': 0,
            'number of blocks with compress ratio smaller than 8': 0,
            'page written failed to compress': 0,
            'page written was too small to compress': 1
          },
          cursor: {
            'Total number of entries skipped by cursor next calls': 0,
            'Total number of entries skipped by cursor prev calls': 0,
            'Total number of entries skipped to position the history store cursor': 0,
            'Total number of times a search near has exited due to prefix config': 0,
            'Total number of times cursor fails to temporarily release pinned page to encourage eviction of hot or large page': 0,
            'Total number of times cursor temporarily releases pinned page to encourage eviction of hot or large page': 0,
            'bulk loaded cursor insert calls': 0,
            'cache cursors reuse count': 11,
            'close calls that result in cache': 12,
            'create calls': 5,
            'cursor bound calls that return an error': 0,
            'cursor bounds cleared from reset': 0,
            'cursor bounds comparisons performed': 0,
            'cursor bounds next called on an unpositioned cursor': 0,
            'cursor bounds next early exit': 0,
            'cursor bounds prev called on an unpositioned cursor': 0,
            'cursor bounds prev early exit': 0,
            'cursor bounds search early exit': 0,
            'cursor bounds search near call repositioned cursor': 0,
            'cursor cache calls that return an error': 0,
            'cursor close calls that return an error': 0,
            'cursor compare calls that return an error': 0,
            'cursor equals calls that return an error': 0,
            'cursor get key calls that return an error': 0,
            'cursor get value calls that return an error': 0,
            'cursor insert calls that return an error': 0,
            'cursor insert check calls that return an error': 0,
            'cursor largest key calls that return an error': 0,
            'cursor modify calls that return an error': 0,
            'cursor next calls that return an error': 0,
            'cursor next calls that skip due to a globally visible history store tombstone': 0,
            'cursor next calls that skip greater than 1 and fewer than 100 entries': 0,
            'cursor next calls that skip greater than or equal to 100 entries': 0,
            'cursor next random calls that return an error': 0,
            'cursor prev calls that return an error': 0,
            'cursor prev calls that skip due to a globally visible history store tombstone': 0,
            'cursor prev calls that skip greater than or equal to 100 entries': 0,
            'cursor prev calls that skip less than 100 entries': 0,
            'cursor reconfigure calls that return an error': 0,
            'cursor remove calls that return an error': 0,
            'cursor reopen calls that return an error': 0,
            'cursor reserve calls that return an error': 0,
            'cursor reset calls that return an error': 0,
            'cursor search calls that return an error': 0,
            'cursor search near calls that return an error': 0,
            'cursor update calls that return an error': 0,
            'insert calls': 200,
            'insert key and value bytes': 13899,
            modify: 0,
            'modify key and value bytes affected': 0,
            'modify value bytes modified': 0,
            'next calls': 95,
            'open cursor count': 0,
            'operation restarted': 0,
            'prev calls': 1,
            'remove calls': 0,
            'remove key bytes removed': 0,
            'reserve calls': 0,
            'reset calls': 26,
            'search calls': 0,
            'search history store calls': 0,
            'search near calls': 0,
            'truncate calls': 0,
            'update calls': 0,
            'update key and value bytes': 0,
            'update value size change': 0
          },
          reconciliation: {
            'VLCS pages explicitly reconciled as empty': 0,
            'approximate byte size of timestamps in pages written': 0,
            'approximate byte size of transaction IDs in pages written': 0,
            'dictionary matches': 0,
            'fast-path pages deleted': 0,
            'internal page key bytes discarded using suffix compression': 0,
            'internal page multi-block writes': 0,
            'leaf page key bytes discarded using prefix compression': 0,
            'leaf page multi-block writes': 0,
            'leaf-page overflow keys': 0,
            'maximum blocks required for a page': 1,
            'overflow values written': 0,
            'page checksum matches': 0,
            'page reconciliation calls': 2,
            'page reconciliation calls for eviction': 0,
            'pages deleted': 0,
            'pages written including an aggregated newest start durable timestamp ': 0,
            'pages written including an aggregated newest stop durable timestamp ': 0,
            'pages written including an aggregated newest stop timestamp ': 0,
            'pages written including an aggregated newest stop transaction ID': 0,
            'pages written including an aggregated newest transaction ID ': 0,
            'pages written including an aggregated oldest start timestamp ': 0,
            'pages written including an aggregated prepare': 0,
            'pages written including at least one prepare': 0,
            'pages written including at least one start durable timestamp': 0,
            'pages written including at least one start timestamp': 0,
            'pages written including at least one start transaction ID': 0,
            'pages written including at least one stop durable timestamp': 0,
            'pages written including at least one stop timestamp': 0,
            'pages written including at least one stop transaction ID': 0,
            'records written including a prepare': 0,
            'records written including a start durable timestamp': 0,
            'records written including a start timestamp': 0,
            'records written including a start transaction ID': 0,
            'records written including a stop durable timestamp': 0,
            'records written including a stop timestamp': 0,
            'records written including a stop transaction ID': 0
          },
          session: { 'object compaction': 0 },
          transaction: {
            'a reader raced with a prepared transaction commit and skipped an update or updates': 0,
            'checkpoint has acquired a snapshot for its transaction': 0,
            'number of times overflow removed value is read': 0,
            'race to read prepared update retry': 0,
            'rollback to stable history store keys that would have been swept in non-dryrun mode': 0,
            'rollback to stable history store records with stop timestamps older than newer records': 0,
            'rollback to stable inconsistent checkpoint': 0,
            'rollback to stable keys removed': 0,
            'rollback to stable keys restored': 0,
            'rollback to stable keys that would have been removed in non-dryrun mode': 0,
            'rollback to stable keys that would have been restored in non-dryrun mode': 0,
            'rollback to stable restored tombstones from history store': 0,
            'rollback to stable restored updates from history store': 0,
            'rollback to stable skipping delete rle': 0,
            'rollback to stable skipping stable rle': 0,
            'rollback to stable sweeping history store keys': 0,
            'rollback to stable tombstones from history store that would have been restored in non-dryrun mode': 0,
            'rollback to stable updates from history store that would have been restored in non-dryrun mode': 0,
            'rollback to stable updates removed from history store': 0,
            'rollback to stable updates that would have been removed from history store in non-dryrun mode': 0,
            'transaction checkpoints due to obsolete pages': 0,
            'update conflicts': 0
          }
        },
        sharded: false,
        size: 13562,
        count: 200,
        numOrphanDocs: 0,
        storageSize: 20480,
        totalIndexSize: 20480,
        totalSize: 40960,
        indexSizes: { _id_: 20480 },
        avgObjSize: 67,
        ns: 'blog_analysis.users',
        nindexes: 1,
        scaleFactor: 1
      }
      blog_analysis>


also

      blog_analysis> db.posts.stats()
      {
        ok: 1,
        capped: false,
        wiredTiger: {
          metadata: { formatVersion: 1 },
          creationString: 'access_pattern_hint=none,allocation_size=4KB,app_metadata=(formatVersion=1),assert=(commit_timestamp=none,durable_timestamp=none,read_timestamp=none,write_timestamp=on),block_allocation=best,block_compressor=snappy,cache_resident=false,checksum=on,colgroups=,collator=,columns=,dictionary=0,encryption=(keyid=,name=),exclusive=false,extractor=,format=btree,huffman_key=,huffman_value=,ignore_in_memory_cache_size=false,immutable=false,import=(compare_timestamp=oldest_timestamp,enabled=false,file_metadata=,metadata_file=,repair=false),internal_item_max=0,internal_key_max=0,internal_key_truncate=true,internal_page_max=4KB,key_format=q,key_gap=10,leaf_item_max=0,leaf_key_max=0,leaf_page_max=32KB,leaf_value_max=64MB,log=(enabled=true),lsm=(auto_throttle=true,bloom=true,bloom_bit_count=16,bloom_config=,bloom_hash_count=8,bloom_oldest=false,chunk_count_limit=0,chunk_max=5GB,chunk_size=10MB,merge_custom=(prefix=,start_generation=0,suffix=),merge_max=15,merge_min=0),memory_page_image_max=0,memory_page_max=10m,os_cache_dirty_max=0,os_cache_max=0,prefix_compression=false,prefix_compression_min=4,source=,split_deepen_min_child=0,split_deepen_per_child=0,split_pct=90,tiered_storage=(auth_token=,bucket=,bucket_prefix=,cache_directory=,local_retention=300,name=,object_target_size=0),type=file,value_format=u,verbose=[write_timestamp],write_timestamp_usage=none',
          type: 'file',
          uri: 'statistics:table:collection-10-8667477942090323950',
          LSM: {
            'bloom filter false positives': 0,
            'bloom filter hits': 0,
            'bloom filter misses': 0,
            'bloom filter pages evicted from cache': 0,
            'bloom filter pages read into cache': 0,
            'bloom filters in the LSM tree': 0,
            'chunks in the LSM tree': 0,
            'highest merge generation in the LSM tree': 0,
            'queries that could have benefited from a Bloom filter that did not exist': 0,
            'sleep for LSM checkpoint throttle': 0,
            'sleep for LSM merge throttle': 0,
            'total size of bloom filters': 0
          },
          autocommit: {
            'retries for readonly operations': 0,
            'retries for update operations': 0
          },
          'block-manager': {
            'allocations requiring file extension': 5,
            'blocks allocated': 5,
            'blocks freed': 0,
            'checkpoint size': 53248,
            'file allocation unit size': 4096,
            'file bytes available for reuse': 0,
            'file magic number': 120897,
            'file major version number': 1,
            'file size in bytes': 69632,
            'minor version number': 0
          },
          btree: {
            'btree checkpoint generation': 1189,
            'btree clean tree checkpoint expiration time': Long("9223372036854775807"),
            'btree compact pages reviewed': 0,
            'btree compact pages rewritten': 0,
            'btree compact pages skipped': 0,
            'btree skipped by compaction as process would not reduce size': 0,
            'column-store fixed-size leaf pages': 0,
            'column-store fixed-size time windows': 0,
            'column-store internal pages': 0,
            'column-store variable-size RLE encoded values': 0,
            'column-store variable-size deleted values': 0,
            'column-store variable-size leaf pages': 0,
            'fixed-record size': 0,
            'maximum internal page size': 4096,
            'maximum leaf page key size': 2867,
            'maximum leaf page size': 32768,
            'maximum leaf page value size': 67108864,
            'maximum tree depth': 3,
            'number of key/value pairs': 0,
            'overflow pages': 0,
            'row-store empty values': 0,
            'row-store internal pages': 0,
            'row-store leaf pages': 0
          },
          cache: {
            'bytes currently in the cache': 280301,
            'bytes dirty in the cache cumulative': 1367,
            'bytes read into cache': 0,
            'bytes written from cache': 171795,
            'checkpoint blocked page eviction': 0,
            'checkpoint of history store file blocked non-history store page eviction': 0,
            'data source pages selected for eviction unable to be evicted': 0,
            'eviction gave up due to detecting a disk value without a timestamp behind the last update on the chain': 0,
            'eviction gave up due to detecting a tombstone without a timestamp ahead of the selected on disk update': 0,
            'eviction gave up due to detecting a tombstone without a timestamp ahead of the selected on disk update after validating the update chain': 0,
            'eviction gave up due to detecting update chain entries without timestamps after the selected on disk update': 0,
            'eviction gave up due to needing to remove a record from the history store but checkpoint is running': 0,
            'eviction walk passes of a file': 0,
            'eviction walk target pages histogram - 0-9': 0,
            'eviction walk target pages histogram - 10-31': 0,
            'eviction walk target pages histogram - 128 and higher': 0,
            'eviction walk target pages histogram - 32-63': 0,
            'eviction walk target pages histogram - 64-128': 0,
            'eviction walk target pages reduced due to history store cache pressure': 0,
            'eviction walks abandoned': 0,
            'eviction walks gave up because they restarted their walk twice': 0,
            'eviction walks gave up because they saw too many pages and found no candidates': 0,
            'eviction walks gave up because they saw too many pages and found too few candidates': 0,
            'eviction walks reached end of tree': 0,
            'eviction walks restarted': 0,
            'eviction walks started from root of tree': 0,
            'eviction walks started from saved location in tree': 0,
            'hazard pointer blocked page eviction': 0,
            'history store table insert calls': 0,
            'history store table insert calls that returned restart': 0,
            'history store table reads': 0,
            'history store table reads missed': 0,
            'history store table reads requiring squashed modifies': 0,
            'history store table resolved updates without timestamps that lose their durable timestamp': 0,
            'history store table truncation by rollback to stable to remove an unstable update': 0,
            'history store table truncation by rollback to stable to remove an update': 0,
            'history store table truncation to remove all the keys of a btree': 0,
            'history store table truncation to remove an update': 0,
            'history store table truncation to remove range of updates due to an update without a timestamp on data page': 0,
            'history store table truncation to remove range of updates due to key being removed from the data page during reconciliation': 0,
            'history store table truncations that would have happened in non-dryrun mode': 0,
            'history store table truncations to remove an unstable update that would have happened in non-dryrun mode': 0,
            'history store table truncations to remove an update that would have happened in non-dryrun mode': 0,
            'history store table updates without timestamps fixed up by reinserting with the fixed timestamp': 0,
            'history store table writes requiring squashed modifies': 0,
            'in-memory page passed criteria to be split': 0,
            'in-memory page splits': 0,
            'internal page split blocked its eviction': 0,
            'internal pages evicted': 0,
            'internal pages split during eviction': 0,
            'leaf pages split during eviction': 0,
            'modified pages evicted': 0,
            'overflow keys on a multiblock row-store page blocked its eviction': 0,
            'overflow pages read into cache': 0,
            'page split during eviction deepened the tree': 0,
            'page written requiring history store records': 0,
            'pages read into cache': 0,
            'pages read into cache after truncate': 0,
            'pages read into cache after truncate in prepare state': 0,
            'pages requested from the cache': 1007,
            'pages seen by eviction walk': 0,
            'pages written from cache': 3,
            'pages written requiring in-memory restoration': 0,
            'recent modification of a page blocked its eviction': 0,
            'reverse splits performed': 0,
            'reverse splits skipped because of VLCS namespace gap restrictions': 0,
            'the number of times full update inserted to history store': 0,
            'the number of times reverse modify inserted to history store': 0,
            'tracked dirty bytes in the cache': 0,
            'uncommitted truncate blocked page eviction': 0,
            'unmodified pages evicted': 0
          },
          cache_walk: {
            'Average difference between current eviction generation when the page was last considered': 0,
            'Average on-disk page image size seen': 0,
            'Average time in cache for pages that have been visited by the eviction server': 0,
            'Average time in cache for pages that have not been visited by the eviction server': 0,
            'Clean pages currently in cache': 0,
            'Current eviction generation': 0,
            'Dirty pages currently in cache': 0,
            'Entries in the root page': 0,
            'Internal pages currently in cache': 0,
            'Leaf pages currently in cache': 0,
            'Maximum difference between current eviction generation when the page was last considered': 0,
            'Maximum page size seen': 0,
            'Minimum on-disk page image size seen': 0,
            'Number of pages never visited by eviction server': 0,
            'On-disk page image sizes smaller than a single allocation unit': 0,
            'Pages created in memory and never written': 0,
            'Pages currently queued for eviction': 0,
            'Pages that could not be queued for eviction': 0,
            'Refs skipped during cache traversal': 0,
            'Size of the root page': 0,
            'Total number of pages currently in cache': 0
          },
          'checkpoint-cleanup': {
            'pages added for eviction': 0,
            'pages removed': 0,
            'pages skipped during tree walk': 0,
            'pages visited': 1
          },
          compression: {
            'compressed page maximum internal page size prior to compression': 4096,
            'compressed page maximum leaf page size prior to compression ': 131072,
            'compressed pages read': 0,
            'compressed pages written': 2,
            'number of blocks with compress ratio greater than 64': 0,
            'number of blocks with compress ratio smaller than 16': 0,
            'number of blocks with compress ratio smaller than 2': 0,
            'number of blocks with compress ratio smaller than 32': 0,
            'number of blocks with compress ratio smaller than 4': 0,
            'number of blocks with compress ratio smaller than 64': 0,
            'number of blocks with compress ratio smaller than 8': 0,
            'page written failed to compress': 0,
            'page written was too small to compress': 1
          },
          cursor: {
            'Total number of entries skipped by cursor next calls': 0,
            'Total number of entries skipped by cursor prev calls': 0,
            'Total number of entries skipped to position the history store cursor': 0,
            'Total number of times a search near has exited due to prefix config': 0,
            'Total number of times cursor fails to temporarily release pinned page to encourage eviction of hot or large page': 0,
            'Total number of times cursor temporarily releases pinned page to encourage eviction of hot or large page': 0,
            'bulk loaded cursor insert calls': 0,
            'cache cursors reuse count': 12,
            'close calls that result in cache': 14,
            'create calls': 7,
            'cursor bound calls that return an error': 0,
            'cursor bounds cleared from reset': 0,
            'cursor bounds comparisons performed': 0,
            'cursor bounds next called on an unpositioned cursor': 0,
            'cursor bounds next early exit': 0,
            'cursor bounds prev called on an unpositioned cursor': 0,
            'cursor bounds prev early exit': 0,
            'cursor bounds search early exit': 0,
            'cursor bounds search near call repositioned cursor': 0,
            'cursor cache calls that return an error': 0,
            'cursor close calls that return an error': 0,
            'cursor compare calls that return an error': 0,
            'cursor equals calls that return an error': 0,
            'cursor get key calls that return an error': 0,
            'cursor get value calls that return an error': 0,
            'cursor insert calls that return an error': 0,
            'cursor insert check calls that return an error': 0,
            'cursor largest key calls that return an error': 0,
            'cursor modify calls that return an error': 0,
            'cursor next calls that return an error': 0,
            'cursor next calls that skip due to a globally visible history store tombstone': 0,
            'cursor next calls that skip greater than 1 and fewer than 100 entries': 0,
            'cursor next calls that skip greater than or equal to 100 entries': 0,
            'cursor next random calls that return an error': 0,
            'cursor prev calls that return an error': 0,
            'cursor prev calls that skip due to a globally visible history store tombstone': 0,
            'cursor prev calls that skip greater than or equal to 100 entries': 0,
            'cursor prev calls that skip less than 100 entries': 0,
            'cursor reconfigure calls that return an error': 0,
            'cursor remove calls that return an error': 0,
            'cursor reopen calls that return an error': 0,
            'cursor reserve calls that return an error': 0,
            'cursor reset calls that return an error': 0,
            'cursor search calls that return an error': 0,
            'cursor search near calls that return an error': 0,
            'cursor update calls that return an error': 0,
            'insert calls': 1000,
            'insert key and value bytes': 167650,
            modify: 0,
            'modify key and value bytes affected': 0,
            'modify value bytes modified': 0,
            'next calls': 95,
            'open cursor count': 0,
            'operation restarted': 0,
            'prev calls': 1,
            'remove calls': 0,
            'remove key bytes removed': 0,
            'reserve calls': 0,
            'reset calls': 30,
            'search calls': 0,
            'search history store calls': 0,
            'search near calls': 0,
            'truncate calls': 0,
            'update calls': 0,
            'update key and value bytes': 0,
            'update value size change': 0
          },
          reconciliation: {
            'VLCS pages explicitly reconciled as empty': 0,
            'approximate byte size of timestamps in pages written': 0,
            'approximate byte size of transaction IDs in pages written': 0,
            'dictionary matches': 0,
            'fast-path pages deleted': 0,
            'internal page key bytes discarded using suffix compression': 2,
            'internal page multi-block writes': 0,
            'leaf page key bytes discarded using prefix compression': 0,
            'leaf page multi-block writes': 1,
            'leaf-page overflow keys': 0,
            'maximum blocks required for a page': 1,
            'overflow values written': 0,
            'page checksum matches': 0,
            'page reconciliation calls': 2,
            'page reconciliation calls for eviction': 0,
            'pages deleted': 0,
            'pages written including an aggregated newest start durable timestamp ': 0,
            'pages written including an aggregated newest stop durable timestamp ': 0,
            'pages written including an aggregated newest stop timestamp ': 0,
            'pages written including an aggregated newest stop transaction ID': 0,
            'pages written including an aggregated newest transaction ID ': 0,
            'pages written including an aggregated oldest start timestamp ': 0,
            'pages written including an aggregated prepare': 0,
            'pages written including at least one prepare': 0,
            'pages written including at least one start durable timestamp': 0,
            'pages written including at least one start timestamp': 0,
            'pages written including at least one start transaction ID': 0,
            'pages written including at least one stop durable timestamp': 0,
            'pages written including at least one stop timestamp': 0,
            'pages written including at least one stop transaction ID': 0,
            'records written including a prepare': 0,
            'records written including a start durable timestamp': 0,
            'records written including a start timestamp': 0,
            'records written including a start transaction ID': 0,
            'records written including a stop durable timestamp': 0,
            'records written including a stop timestamp': 0,
            'records written including a stop transaction ID': 0
          },
          session: { 'object compaction': 0 },
          transaction: {
            'a reader raced with a prepared transaction commit and skipped an update or updates': 0,
            'checkpoint has acquired a snapshot for its transaction': 0,
            'number of times overflow removed value is read': 0,
            'race to read prepared update retry': 0,
            'rollback to stable history store keys that would have been swept in non-dryrun mode': 0,
            'rollback to stable history store records with stop timestamps older than newer records': 0,
            'rollback to stable inconsistent checkpoint': 0,
            'rollback to stable keys removed': 0,
            'rollback to stable keys restored': 0,
            'rollback to stable keys that would have been removed in non-dryrun mode': 0,
            'rollback to stable keys that would have been restored in non-dryrun mode': 0,
            'rollback to stable restored tombstones from history store': 0,
            'rollback to stable restored updates from history store': 0,
            'rollback to stable skipping delete rle': 0,
            'rollback to stable skipping stable rle': 0,
            'rollback to stable sweeping history store keys': 0,
            'rollback to stable tombstones from history store that would have been restored in non-dryrun mode': 0,
            'rollback to stable updates from history store that would have been restored in non-dryrun mode': 0,
            'rollback to stable updates removed from history store': 0,
            'rollback to stable updates that would have been removed from history store in non-dryrun mode': 0,
            'transaction checkpoints due to obsolete pages': 0,
            'update conflicts': 0
          }
        },
        sharded: false,
        size: 165713,
        count: 1000,
        numOrphanDocs: 0,
        storageSize: 69632,
        totalIndexSize: 28672,
        totalSize: 98304,
        indexSizes: { _id_: 28672 },
        avgObjSize: 165,
        ns: 'blog_analysis.posts',
        nindexes: 1,
        scaleFactor: 1
      }
      blog_analysis>

<a name="28"></a>
### Exploring the data

<a name="29"></a>
#### Sorting 
To sort in the MongoDB Compass:

![](https://github.com/DanialArab/images/blob/main/NoSQL/sort.PNG)

to get the same sorting but using the MongoDB Shell:

      blog_analysis> db.posts.find().sort({likes: -1})
      [
        {
          _id: ObjectId("5c9fee8966d8c1392df11009"),
          post_id: 349,
          user_id: 72,
          body: 'Lorem ipsum dolor sit amet',
          topic: 'music',
          likes: 500,
          dislikes: 300,
          views: 808,
          date_created: ISODate("2018-07-12T12:08:12.000Z")
        },
        {
          _id: ObjectId("5c9fee8a66d8c1392df1110f"),
          post_id: 611,
          user_id: 95,
          body: 'Aliquam eget suscipit odio',
          topic: 'gaming',
          likes: 500,
          dislikes: 42,
          views: 588,
          date_created: ISODate("2018-05-29T05:08:50.000Z")
        },
        {
          _id: ObjectId("5c9fee8a66d8c1392df111e4"),
          post_id: 824,
          user_id: 6,
          body: 'consectetur adipiscing elit',
          topic: 'politics',
          likes: 500,
          dislikes: 95,
          views: 711,
          date_created: ISODate("2018-02-01T02:28:58.000Z")
        }
        ]
      Type "it" for more
      blog_analysis>

<a name="30"></a>
#### Projection 

This will allow us to only return certain fields back for each document that we're querying. To do so in the MongoDB Compass

![](https://github.com/DanialArab/images/blob/main/NoSQL/projection.PNG)

The primary key **_id** is always included by default. 

To get the same but using the MongoDB Shell:


      blog_analysis> db.posts.find({}, {likes: 1})
      [
        { _id: ObjectId("5c9fee8966d8c1392df10ead"), likes: 168 },
        { _id: ObjectId("5c9fee8966d8c1392df10eae"), likes: 334 },
        { _id: ObjectId("5c9fee8966d8c1392df10eaf"), likes: 403 },
        { _id: ObjectId("5c9fee8966d8c1392df10eb0"), likes: 488 },
        { _id: ObjectId("5c9fee8966d8c1392df10eb1"), likes: 164 },
        { _id: ObjectId("5c9fee8966d8c1392df10eb2"), likes: 119 },
        { _id: ObjectId("5c9fee8966d8c1392df10eb3"), likes: 428 },
        { _id: ObjectId("5c9fee8966d8c1392df10eb4"), likes: 20 },
        { _id: ObjectId("5c9fee8966d8c1392df10eb5"), likes: 449 },
        { _id: ObjectId("5c9fee8966d8c1392df10eb6"), likes: 132 },
        { _id: ObjectId("5c9fee8966d8c1392df10eb7"), likes: 238 },
        { _id: ObjectId("5c9fee8966d8c1392df10eb8"), likes: 167 },
        { _id: ObjectId("5c9fee8966d8c1392df10eb9"), likes: 65 },
        { _id: ObjectId("5c9fee8966d8c1392df10eba"), likes: 79 },
        { _id: ObjectId("5c9fee8966d8c1392df10ebb"), likes: 344 },
        { _id: ObjectId("5c9fee8966d8c1392df10ebc"), likes: 323 },
        { _id: ObjectId("5c9fee8966d8c1392df10ebd"), likes: 98 },
        { _id: ObjectId("5c9fee8966d8c1392df10ebe"), likes: 427 },
        { _id: ObjectId("5c9fee8966d8c1392df10ebf"), likes: 495 },
        { _id: ObjectId("5c9fee8966d8c1392df10ec0"), likes: 220 }
      ]
      Type "it" for more
      blog_analysis>

or

      blog_analysis> db.posts.find({}, {likes: 1, dislikes: 1})
      [
        {
          _id: ObjectId("5c9fee8966d8c1392df10ead"),
          likes: 168,
          dislikes: 341
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10eae"),
          likes: 334,
          dislikes: 47
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10eaf"),
          likes: 403,
          dislikes: 293
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10eb0"),
          likes: 488,
          dislikes: 60
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10eb1"),
          likes: 164,
          dislikes: 161
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10eb2"),
          likes: 119,
          dislikes: 487
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10eb3"),
          likes: 428,
          dislikes: 130
      blog_analysis>
        {
          _id: ObjectId("5c9fee8966d8c1392df10eb4"),
          likes: 20,
          dislikes: 431
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10eb5"),
          likes: 449,
          dislikes: 78
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10eb6"),
          likes: 132,
          dislikes: 272
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10eb7"),
          likes: 238,
          dislikes: 229
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10eb8"),
          likes: 167,
          dislikes: 75
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10eb9"),
          likes: 65,
          dislikes: 153
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10eba"),
          likes: 79,
          dislikes: 383
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10ebb"),
          likes: 344,
          dislikes: 175
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10ebc"),
          likes: 323,
          dislikes: 379
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10ebd"),
          likes: 98,
          dislikes: 446
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10ebe"),
          likes: 427,
          dislikes: 78
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10ebf"),
          likes: 495,
          dislikes: 188
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10ec0"),
          likes: 220,
          dislikes: 211
        }
      ]
      Type "it" for more
      blog_analysis>

<a name="31"></a>
#### Filter

How to get the posts with the number of likes graeter than the midpoints (min of likes is 1 and the max of likes is 500 so the midpoint is 251), in the MongoDB Compass:

![](https://github.com/DanialArab/images/blob/main/NoSQL/filter.PNG)

to do the same but using the MongoDB Shell:

      blog_analysis> db.posts.aggregate([
      ...   {
      ...     $match: {
      ...       likes: { $gte: 251 }
      ...     }
      ...   },
      ...   {
      ...     $sort: {
      ...       likes: -1
      ...     }
      ...   }
      ... ])
      [
        {
          _id: ObjectId("5c9fee8966d8c1392df11009"),
          post_id: 349,
          user_id: 72,
          body: 'Lorem ipsum dolor sit amet',
          topic: 'music',
          likes: 500,
          dislikes: 300,
          views: 808,
          date_created: ISODate("2018-07-12T12:08:12.000Z")
        },
        {
          _id: ObjectId("5c9fee8a66d8c1392df1110f"),
          post_id: 611,
          user_id: 95,
          body: 'Aliquam eget suscipit odio',
          topic: 'gaming',
          likes: 500,
          dislikes: 42,
          views: 588,
          date_created: ISODate("2018-05-29T05:08:50.000Z")
        },
        {
          _id: ObjectId("5c9fee8a66d8c1392df111e4"),
          post_id: 824,
          user_id: 6,
          body: 'consectetur adipiscing elit',
          topic: 'politics',
          likes: 500,
          dislikes: 95,
          views: 711,
          date_created: ISODate("2018-02-01T02:28:58.000Z")
        },
        {
          _id: ObjectId("5c9fee8a66d8c1392df1120b"),
          post_id: 863,
          user_id: 118,
          body: 'ut elementum urna malesuada',
          topic: 'health',
          likes: 500,
          dislikes: 70,
          views: 665,
          date_created: ISODate("2018-11-17T01:40:10.000Z")
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10ee4"),
          post_id: 56,
          user_id: 102,
          body: 'consectetur adipiscing elit',
          topic: 'politics',
          likes: 499,
          dislikes: 370,
          views: 983,
          date_created: ISODate("2018-09-29T10:18:13.000Z")
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10f8a"),
          post_id: 222,
          user_id: 6,
          body: 'Quisque semper justo libero',
          topic: 'sports',
          likes: 499,
          dislikes: 8,
          views: 582,
          date_created: ISODate("2018-11-06T11:42:50.000Z")
        },
        {
          _id: ObjectId("5c9fee8a66d8c1392df111a5"),
          post_id: 761,
          user_id: 58,
          body: 'Proin ornare augue ex, a interdum nulla porttitor quis',
          topic: 'sports',
          likes: 499,
          dislikes: 435,
          views: 1102,
          date_created: ISODate("2018-08-06T02:02:41.000Z")
        },
        {
          _id: ObjectId("5c9fee8a66d8c1392df111ad"),
          post_id: 769,
          user_id: 64,
          body: 'Nullam nunc dolor',
          topic: 'sports',
          likes: 499,
          dislikes: 210,
          views: 939,
          date_created: ISODate("2018-05-30T23:24:04.000Z")
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10f0c"),
          post_id: 96,
          user_id: 168,
          body: 'Nullam nunc dolor',
          topic: 'health',
          likes: 498,
          dislikes: 316,
          views: 1061,
          date_created: ISODate("2018-11-11T08:04:17.000Z")
        },
        {
          _id: ObjectId("5c9fee8a66d8c1392df11133"),
          post_id: 647,
          user_id: 114,
          body: 'Nullam a viverra magna',
          topic: 'sports',
          likes: 497,
          dislikes: 428,
          views: 1081,
          date_created: ISODate("2018-04-06T22:28:59.000Z")
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10fa6"),
          post_id: 250,
          user_id: 148,
          body: 'Nullam dictum dapibus magna quis elementum',
          topic: 'health',
          likes: 496,
          dislikes: 273,
          views: 909,
          date_created: ISODate("2018-11-29T14:04:15.000Z")
        },
        {
          _id: ObjectId("5c9fee8a66d8c1392df11273"),
          post_id: 967,
          user_id: 105,
          body: 'ut elementum urna malesuada',
          topic: 'politics',
          likes: 496,
          dislikes: 181,
          views: 750,
          date_created: ISODate("2018-09-18T20:39:50.000Z")
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10ebf"),
          post_id: 19,
          user_id: 167,
          body: 'Nullam a viverra magna',
          topic: 'gaming',
          likes: 495,
          dislikes: 188,
          views: 819,
          date_created: ISODate("2018-10-19T16:39:50.000Z")
        },
        {
          _id: ObjectId("5c9fee8a66d8c1392df11217"),
          post_id: 875,
          user_id: 166,
          body: 'Nullam a viverra magna',
          topic: 'politics',
          likes: 495,
          dislikes: 446,
          views: 1160,
          date_created: ISODate("2018-05-02T13:25:42.000Z")
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10fe6"),
          post_id: 314,
          user_id: 51,
          body: 'Suspendisse finibus erat nec ipsum commodo',
          topic: 'health',
          likes: 494,
          dislikes: 113,
          views: 701,
          date_created: ISODate("2018-10-02T09:57:21.000Z")
        },
        {
          _id: ObjectId("5c9fee8a66d8c1392df11051"),
          post_id: 421,
          user_id: 195,
          body: 'Quisque semper justo libero',
          topic: 'gaming',
          likes: 494,
          dislikes: 108,
          views: 721,
          date_created: ISODate("2018-05-07T10:28:15.000Z")
        },
        {
          _id: ObjectId("5c9fee8a66d8c1392df1105f"),
          post_id: 435,
          user_id: 17,
          body: 'consectetur adipiscing elit',
          topic: 'sports',
          likes: 494,
          dislikes: 146,
          views: 830,
          date_created: ISODate("2018-02-26T10:58:11.000Z")
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10f76"),
          post_id: 202,
          user_id: 99,
          body: 'Nullam nunc dolor',
          topic: 'sports',
          likes: 493,
          dislikes: 228,
          views: 868,
          date_created: ISODate("2018-05-04T16:41:05.000Z")
        },
        {
          _id: ObjectId("5c9fee8966d8c1392df10f3d"),
          post_id: 145,
          user_id: 109,
          body: 'Aliquam eget suscipit odio',
          topic: 'gaming',
          likes: 492,
          dislikes: 393,
          views: 1098,
          date_created: ISODate("2018-11-16T21:44:14.000Z")
        },
        {
          _id: ObjectId("5c9fee8a66d8c1392df111c1"),
          post_id: 789,
          user_id: 31,
          body: 'Quisque semper justo libero',
          topic: 'sports',
          likes: 492,
          dislikes: 492,
          views: 1054,
          date_created: ISODate("2018-09-26T13:45:14.000Z")
        }
      ]
      Type "it" for more
      blog_analysis>
      
For the Date object, the query is a bit different and it is like:

      {date_created : {$gte : new Date ('2018-07-01')}}

in the MongoDB Compass is:

![](https://github.com/DanialArab/images/blob/main/NoSQL/filter_date.PNG)

To get the distribution of data with respect to the topics that we have in the dataset:

In the MongoDB Compass:

![](https://github.com/DanialArab/images/blob/main/NoSQL/filter_by_topic.PNG)

In the MongoDB Shell:

      blog_analysis> db.posts.find({topic: 'sports'}).count()
      188

to get all the topics:

      blog_analysis> db.posts.distinct('topic')
      [ 'gaming', 'health', 'music', 'politics', 'sports' ]
      blog_analysis>

also:

      blog_analysis> db.posts.find({topic: 'gaming'}).count()
      187
      blog_analysis> db.posts.find({topic: 'music'}).count()
      196
      blog_analysis> db.posts.find({topic: 'health'}).count()
      218
      blog_analysis> db.posts.find({topic: 'politics'}).count()
      211


<a name="32"></a>
### Identifying correlations in data

Multiple conditions at the same time:

In the MongoDB Compass:

![](https://github.com/DanialArab/images/blob/main/NoSQL/double_filtered.PNG)

In the MongoDB Shell:

      blog_analysis> db.posts.find({$and: [{date_created: {$lt: new Date ('2018-07-01')}}, {likes: {$gte: 251}}]}).count()
      234
      blog_analysis>



