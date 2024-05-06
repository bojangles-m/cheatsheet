# MongoDB Cheat Sheet

## Install & Setup

```
$ brew tap mongodb/brew
$ brew install mongodb-community
$ brew services start mongodb-community

# If you have a previous version of mongodb
$ brew services stop mongodb
$ brew uninstall mongodb

mongod --config /usr/local/etc/mongod.conf

/usr/local/var/log/mongodb/mongo.log
```

## Trouble shooting

```
Had the same problem and it could be due to your service not being able to create the socket (check with netstat -an | grep 27017 if you have it up properly)

What I did:

Create a properly placed data/db on System/Volumes/Data/data/db, with

sudo mkdir -p /System/Volumes/Data/data/db
sudo chown -R `id -un` /System/Volumes/Data/data/db
And, then, add that path to mongod.conf (located on /usr/local/etc/mongod.conf), replacing dbPath there:

...
storage:
  dbPath: /System/Volumes/Data/data/db
...
Then, restart it. If you are using brew, do:

brew services restart mongodb-community
Source: https://zellwk.com/blog/install-mongodb/
```

## Misc

Run mongo server with node

```
nodemon server.js (run on server.js script in your app)
```

Execute a JavaScript file form CLI

```
mongo 127.0.0.1:27017/dcm mongo.init.js
```

Connect to mongodb in bash

```
mongo
```

## Shell commands

Show All Databases

```
show dbs
```

Show Current Database

```
db
```

Create Or Switch Database

```
use acme
```

Drop

```
db.dropDatabase()
```

Create Collection

```
db.createCollection('posts')
```

Show Collections

```
show collections
```

Insert Row

```
db.posts.insert({
  title: 'Post One',
  body: 'Body of post one',
  category: 'News',
  tags: ['news', 'events'],
  user: {
    name: 'John Doe',
    status: 'author'
  },
  date: Date()
})
```

Insert Multiple Rows

```
db.posts.insertMany([
  {
    title: 'Post Two',
    body: 'Body of post two',
    category: 'Technology',
    date: Date()
  },
  {
    title: 'Post Three',
    body: 'Body of post three',
    category: 'News',
    date: Date()
  },
  {
    title: 'Post Four',
    body: 'Body of post three',
    category: 'Entertainment',
    date: Date()
  }
])
```

Get All Rows

```
db.posts.find()
```

Get All Rows Formatted

```
db.find().pretty()
```

Find Rows

```
db.posts.find({ category: 'News' })
```

Sort Rows

```
# asc
db.posts.find().sort({ title: 1 }).pretty()
# desc
db.posts.find().sort({ title: -1 }).pretty()
```

Count Rows

```
db.posts.find().count()
db.posts.find({ category: 'news' }).count()
```

Limit Rows

```
db.posts.find().limit(2).pretty()
```

Chaining

```
db.posts.find().limit(2).sort({ title: 1 }).pretty()
```

Foreach

```
db.posts.find().forEach(function(doc) {
  print("Blog Post: " + doc.title)
})
```

Find One Row

```
db.posts.findOne({ category: 'News' })
```

Find Specific Fields

```
db.posts.find({ title: 'Post One' }, {
  title: 1,
  author: 1
})
```

Update Row

```
db.posts.update({ title: 'Post Two' },
{
  title: 'Post Two',
  body: 'New body for post 2',
  date: Date()
},
{
  upsert: true
})
```

Update Specific Field

```
db.posts.update({ title: 'Post Two' },
{
  $set: {
    body: 'Body for post 2',
    category: 'Technology'
  }
})
```

Increment Field (\$inc)

```
db.posts.update({ title: 'Post Two' },
{
  $inc: {
    likes: 5
  }
})
```

Rename Field

```
db.posts.update({ title: 'Post Two' },
{
  $rename: {
    likes: 'views'
  }
})
```

Remove filed 'category' in One or in All posts

```
db.posts.update({ title: 'Post Two' },
{
  $unset: {
    category: ""
  }
})

db.posts.update({},
{
  $unset: {
    category: 1
  }
}, false, true)
```

Delete Row

```
db.posts.remove({ title: 'Post Four' })
```

Sub-Documents

```
db.posts.update({ title: 'Post One' },
{
  $set: {
    comments: [
      {
        body: 'Comment One',
        user: 'Mary Williams',
        date: Date()
      },
      {
        body: 'Comment Two',
        user: 'Harry White',
        date: Date()
      }
    ]
  }
})
```

Find By Element in Array (\$elemMatch)

```
db.posts.find({
  comments: {
     $elemMatch: {
       user: 'Mary Williams'
       }
    }
  }
)
```

Add Index

```
db.posts.createIndex({ title: 'text' })
```

Text Search

```
db.posts.find({
  $text: {
    $search: "\"Post O\""
    }
})
```

Greater & Less Than

```
db.posts.find({ views: { $gt: 2 } })
db.posts.find({ views: { $gte: 7 } })
db.posts.find({ views: { $lt: 7 } })
db.posts.find({ views: { $lte: 7 } })
```
