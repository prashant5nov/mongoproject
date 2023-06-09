# MONGO SETUP

### To run `mongodb`
brew services start mongodb-community@6.0

### To stop `mongodb`
brew services stop mongodb-community@6.0

### To run `mongodb` as background process
mongod --config /opt/homebrew/etc/mongod.conf --fork

### To restart
brew services restart mongodb/brew/mongodb-community

### To run mongo shell
mongosh

## To start Mongo shell

At start, add `docker-compose.yaml` file in your project root.
And then run following commands - 
```bash

# execute following command for the first time
docker-compose up -d mongo

# To list all running containers
docker ps

# execute following command for the next time
docker exec -it mongoproject-mongo-1 mongosh                   

# In above command `mongoproject-mongo-1` should be name that reflects in `docker ps`
```

NOTE - 
If `mongosh` command is not working for non-docker users then they need 
to set up PATH variable. Refer - https://www.mongodb.com/docs/mongodb-shell/install/#install-from-.zip-file


# MONGO Commands

#### To get list of existing databases
```bash
show databases
```
#### To get help
```bash
.help
```
#### To use existing or create new database
```bash
use films
```
#### To insert a single record in database
```bash
db.films.insertOne({"title": "My Film", "year": 2023, "watched": false})
```

#### To get list of all the records in given table
```bash
db.films.find()
```

#### To get single record (by default this command returns the oldest record)
```bash
db.films.findOne()
```

#### To filter out records based on certain column
```bash
db.films.find({"title": "My Film"})
db.films.find({"year": 2023})
```

#### To filter out records based id
```bash
db.films.findOne({"_id": ObjectId("640c62845792975afc98eb32")})
```

#### To get records in descending order
```bash
db.films.find().sort({"year": -1})
```

#### To get only certain fields from any given record
```bash
db.films.find({}, {"title": 1, "year": 1})
```

#### To exclude certain field in output
```bash
db.films.find({}, {"title": 0})

```

NOTE - we cannot use selection and exclusion in same query.
For example it will be invalid to say - `db.films.find({}, {"title": 1, "year": 0})`

#### To insert multiple films in single shot
```bash
db.films.insertMany() # list of films should be provided as input
db.films.insertMany([{"title":"spiderman","year":2018,"watched":false},{"title":"avengers","year":2022,"watched":false},{"title":"starwars","year":2023,"watched":true},{"title":"randomfilm","year":2001,"watched":true}])
```

#### To get films produced before/after 2021
```bash
db.films.findOne({"year": {"$gt": 2021}})
db.films.find({"year": {"$gt": 2021}})
db.films.findOne({"year": {"$lt": 2021}})
db.films.find({"year": {"$lt": 2021}})
```

#### To get count of records
```bash
db.films.countDocuments()
```

#### To get all the films but skip 1 
```bash
db.films.find().skip(1)  # oldest record is skipped
```


#### To delete a record
```bash
db.films.deleteOne({"_id": ObjectId("640c62845792975afc98eb31")})
```
#### To update records
```bash
db.films.updateOne({"_id": ObjectId("640c62845792975afc98eb33")}, {$set: {"year": 2018}})
```

