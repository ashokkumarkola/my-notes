# MongoDB Cheat Sheet

## Terms

| SQL | MongoDB |
|---|---|
| Database | Database |
| Table | Collection |
| Row | Document (BSON/JSON) |
| Column | Field |
| Primary key | `_id` (auto `ObjectId`) |
| Join | `$lookup` / embedding |

## Run + connect

```bash
docker run -d --name mongo -p 27017:27017 mongo:7
mongosh                                         # localhost:27017
mongosh "mongodb://user:pass@localhost:27017/mydb"
```

## Shell basics

```javascript
show dbs
use mydb                     // switch / create on first write
show collections
db.users.drop()
db.dropDatabase()
```

## CRUD

```javascript
db.users.insertOne({ name: "a", age: 20, tags: ["dev"] })
db.users.insertMany([{ name: "b" }, { name: "c" }])

db.users.find()
db.users.find({ age: { $gte: 18 } }, { name: 1, _id: 0 })   // filter, projection
db.users.findOne({ name: "a" })
db.users.find().sort({ age: -1 }).limit(10).skip(20)
db.users.countDocuments({ age: { $gt: 18 } })

db.users.updateOne({ name: "a" }, { $set: { age: 21 } })
db.users.updateMany({}, { $inc: { age: 1 } })
db.users.updateOne({ name: "z" }, { $set: { age: 1 } }, { upsert: true })

db.users.deleteOne({ name: "a" })
db.users.deleteMany({ age: { $lt: 18 } })
```

## Operators

| Type | Operators |
|---|---|
| Compare | `$eq` `$ne` `$gt` `$gte` `$lt` `$lte` `$in` `$nin` |
| Logic | `$and` `$or` `$not` `$nor` |
| Element | `$exists` `$type` |
| Array | `$all` `$elemMatch` `$size` |
| Update | `$set` `$unset` `$inc` `$push` `$pull` `$addToSet` |
| Text | `$regex` |

## Indexes

```javascript
db.users.createIndex({ email: 1 }, { unique: true })
db.users.createIndex({ age: 1, name: -1 })      // compound
db.users.getIndexes()
db.users.find({ email: "a@x.com" }).explain("executionStats")
```

## Aggregation

```javascript
db.orders.aggregate([
  { $match: { status: "paid" } },
  { $group: { _id: "$userId", total: { $sum: "$amount" } } },
  { $sort: { total: -1 } },
  { $limit: 5 },
  { $lookup: { from: "users", localField: "_id", foreignField: "_id", as: "user" } }
])
```

Stages: `$match` `$group` `$project` `$sort` `$limit` `$skip` `$unwind` `$lookup` `$count`.

## Backup / restore

```bash
mongodump --db mydb --out ./backup
mongorestore --db mydb ./backup/mydb
mongoexport --db mydb --collection users --out users.json
mongoimport --db mydb --collection users --file users.json
```
