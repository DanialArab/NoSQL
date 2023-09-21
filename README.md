# NoSQL

Reference: <a href="https://www.udemy.com/course/introduction-to-mongodb/?utm_source=adwords-learn&utm_medium=udemyads&utm_campaign=DSA_CA_Tech&utm_content=deal4584&utm_term=_._ag_76808851565_._ad_533102607579_._de_c_._dm__._pl__._ti_dsa-796176360685_._li_9001497_._pd__._&gclid=Cj0KCQjw06-oBhC6ARIsAGuzdw0YatK9S42zHe7Ml6tPW_MBmrBcWXUeE-W43oxmwKPiGX_L3Qq5EJ8aApJPEALw_wcB
">Introduction to MongoDB for Data Analytics  </a>

1. [Introduction](#1)
2. 

<a name="1"></a>
## Introduction

NoSQL = Not only SQL

![](https://github.com/DanialArab/images/blob/main/NoSQL/sql%20vs%20nosql%200.PNG)

![](https://github.com/DanialArab/images/blob/main/NoSQL/sql%20vs%20nosql%202.PNG)

+ **Schema is a mapping of the structure of your data**. It will tell you how many columns you'll have in a table for example what type of data each column will store and things like that
  In SQL, The schema is **predetermined** when your database is created. And so changing your schema after the fact is very difficult. And one thing that this means is that you need to do a bunch of **prep work upfront to define the exact schema that you will**. And this won't necessarily be the case with no sequel because it no sequel your schema is not predefined.
+ So in our sequel example one of the blog posts has no dislikes and then the other has no likes in sequel because **all of our data has to have the same structure**, each of these posts would have to have a likes field and a dislikes field but because in **no sequel our schema is flexible**, We don't have to have the same exact keys and values for every document. We could just not include a dislikes field for the post that doesn't have any dislikes. And then we could also leave out the likes field for this post that has no likes
+ In a SQL table each row in that table needs to have the same columns/attributes as all the other rows in the table. B**ut you can't have one row have an extra column that another row does not have while in MongoDB each collection can have documents that have different structures not every document in a collection has to have the same keys or the same number of keys as another.**
+ In MongoDB, we can do something very interesting. We can combine our post and the comments that go with a blog post into a single document. And this means that rather than needing to have separate tables or in the case of Mongo D.B. separate collections for posts and their comments we can have a single collection that stores everything:
  
![](https://github.com/DanialArab/images/blob/main/NoSQL/sql.PNG)

![](https://github.com/DanialArab/images/blob/main/NoSQL/nosql.PNG)
