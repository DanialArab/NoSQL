# NoSQL

NoSQL = Not only SQL

![](https://github.com/DanialArab/images/blob/main/NoSQL/sql%20vs%20nosql%201.PNG)

![](https://github.com/DanialArab/images/blob/main/NoSQL/sql%20vs%20nosql%202.PNG)

+ Schema is a mapping of the structure of your data. It will tell you how many columns you'll have in a table for example what type of data each column will store and things like that with sequel The schema is predetermined when your database is created. And so changing your schema after the fact is very difficult. And one thing that this means is that you need to do a bunch of prep work upfront to define the exact schema that you will need. And this won't necessarily be the case with no sequel because it no sequel your schema is not predefined.
+ So in our sequel example one of the blog posts has no dislikes and then the other has no likes in sequel

because all of our data has to have the same structure.

Each of these posts would have to have a likes field and a dislikes field but because in no sequel our

schema is flexible.

We don't have to have the same exact keys and values for every document.

We could just not include a dislikes field for the post that doesn't have any dislikes.

And then we could also leave out the likes field for this post that has no likes and just to reiterate

in a sequel table each row in that table needs to have the same columns and needs to have the same attributes

as all the other rows in the table not the same values.

But you can't have one row have an extra column that another road does not have while in Mongo D.B.

each collection can have documents that have different structures not every document in a collection

has to have the same keys or the same number of keys as another.
