# MongoDB Atlas Workshop
#### Date: January 30, 2019 `[9AM - 2PM]`

## Summary
**Supported Cloud Services for full deployment:** AWS, GCP, and Azure

Similarly to **MongoDB Operations Manager**, clusters can be detected in an existing environment for continuous integration.
___
[Workshop Slides](https://github.com/charlespetchsy/mongodb-atlas-workshop/blob/master/slides/MongoDB-Workshop-Toronto%201_2019.pdf) <br>
You can deploy a sharded cluster with **MongoDB Atlas** without the technical hassle of manually configuring it. An additional tool called **MongoDB Compass** is a schema visualizer that helps you execute queries without accessing the command-line prompt.

**MongoDB Stitch** is a framework that deploys web applications with the control of Atlas and Compass for the back-end.

**All of these applications can work in a dockerized environment with a few extra steps.

## Basic CRUD Operations ( Review )

**Assumptions:** Create a database with the collection name `movies`.

### CREATE
Insert a single entity:
```
db.movies.insertOne({
   "title": "Ghostbusters",
   "Year": 1984,
   "Rated": "PG",
   "Runtime": 105,
   "Type": "movie",
   "Genres": ["comedy", "action"] ,
   "Director": "Ivan Reitman",
   "Writers": ["dan aykroyd", "Harold ramis"]
})
```

### READ
Find a single entity: `db.movies.findOne()` <br>
Find and format output: `db.movies.find().pretty()`

### UPDATE
Update the record with a movie rating:
```
db.movies.updateOne({
	title: "Ghostbusters"
    },
    {
	  $set: {
  	    imdb: { id: "tt0087332", rating: 7.8, votes: 312798 }
	}
})
```

### DELETE
Delete the entity:
```
db.movies.deleteOne({
	title: "Ghostbusters"
})
```

## Crud Exercise Solutions
| Question | Query String |
|----------|--------------|
| From 1987 | `db.movies.find( { year : 1987 } )` |
| "Comedy” as one of their genres | `db.movies.find( { genres : "Comedy" } )` |
| "Comedy" as only genre | `db.movies.find( { genres : [ "Comedy" ] } )` |
| "Comedy" or "Drama" | `db.movies.find( { genres : { $in : [ "Comedy", "Drama" ] } } )` |
| "Comedy" and "Drama" | `db.movies.find( { genres : { $all : [ "Comedy", "Drama" ] } } )` |
| IMDB Rating>8.0 and PG Rating | `db.movies.find( { "imdb.rating" : { $gt : 8.0 }, rated : "PG" } )` |
| Title starting with “Dr. Strangelove” | `db.movies.find( { title : { $regex: '^Dr. Strangelove' } } )` |

## Aggregation Exercise Solutions
| Question | Query String |
|----------|--------------|
| How can you use $match to find all comedies? | `$match { genres: "Comedy" }` |
| How can you use $unwind to create an individual document for each country? | `$unwind { path : "$countries" }` |
| How can you use $group to count all the comedies grouped by country? | `$group { _id: "$countries", count: { $sum:1 } }`
 |

## MongoDB Stitch Workshop

Stitch Examples can be found [here](https://github.com/mongodb/stitch-examples/
). <br>
`git clone https://github.com/mongodb/stitch-examples.git`

___
![alt text](https://github.com/charlespetchsy/mongodb-atlas-workshop/blob/master/screens/mongo-charts.png)
