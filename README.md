# My Programming Cheatsheets

Putting things in this file helps me to synthetize and see if I really understood concepts I've learned during my learning journey.
It can also useful as a reminder and mini tutos.
I know the title of this file not really suits its purpose ;)
Initially, it was really about doing a cheatsheet, but when I realize how benefic it was for my comprehension, I drift a bit :)

---

## Summary

- [Flowchart and Pseudocode](#flowchart-and-pseudocode)
- [Shell](#shell)
- [Git](#git)
- [RegEx](#regex)
- [Docker](#docker)
- [Python](#python)
- [HTML](#html)
- [CSS](#css)
- [Javascript](#javascript)
- [SQL](#sql)
- [MongoDB](#mongodb)

---

## MongoDB

[Back to summary](#summary)

- [Mongo Shell](#mongo-shell)

### CRUD operations

- [Create](#create)
- [Read](#read)
- [Update](#update)
- [Delete](#delete)

### ODM

- [Mongoose](#mongoose)

---

### Mongo Shell

[Back to summary](#mongodb)  
open mongo shell

```shell
mongo
```

Commands list

```shell
help
```

Show Databases, collections, users...

```shell
show dbs
show collections
show users
```

Switch to a specific database (create it if doesn't exist)

```shell
use db_name
```

To show in which DB you currently are

```shell
db
```

---

### Create

[Back to summary](#mongodb)

- db.collection.insertOne() inserts a single document into a collection. If the document does not specify an \_id field, MongoDB adds the \_id field with an ObjectId value to the new document.

```javascript
db.movies.insertOne(
  // If the movies collection (SQL table equivalent)
  {
    // doesn't exist, it will be created
    title: "The Favourite",
    genres: ["Drama", "History"],
    runtime: 121,
    rated: "R",
    year: 2018,
    directors: ["Yorgos Lanthimos"],
    cast: ["Olivia Colman", "Emma Stone", "Rachel Weisz"],
    type: "movie",
  }
);
```

- db.collection.insertMany() can insert multiple documents into a collection. Pass an array of documents to the method. If the documents do not specify an \_id field, MongoDB adds the \_id field with an ObjectId value to each document

```javascript
db.movies.insertMany([
  {
    title: "Jurassic World: Fallen Kingdom",
    genres: ["Action", "Sci-Fi"],
    runtime: 130,
    rated: "PG-13",
    year: 2018,
    directors: ["J. A. Bayona"],
    cast: ["Chris Pratt", "Bryce Dallas Howard", "Rafe Spall"],
    type: "movie",
  },
  {
    title: "Tag",
    genres: ["Comedy", "Action"],
    runtime: 105,
    rated: "R",
    year: 2018,
    directors: ["Jeff Tomsic"],
    cast: ["Annabelle Wallis", "Jeremy Renner", "Jon Hamm"],
    type: "movie",
  },
]);
```

---

### Read

[Back to summary](#mongodb)

- Use the db.collection.find() method in the MongoDB Shell to query documents in a collection. To read all documents in the collection, pass an empty document as the query filter parameter to the find method.

```javascript
db.movies.find(); // all
db.accounts.findOne({ account_id: 893421 }); // One
```

- To select documents which match an equality condition, specify the condition as a "field: value" pair in the query filter document.

```javascript
db.movies.find({
  title: "Titanic",
});
```

- Use [query operators](https://docs.mongodb.com/manual/reference/operator/query/#query-selectors) in a query filter document to perform more complex comparisons and evaluations. Query operators in a query filter document have the following form: { field1: { operator1: value1 }, ... }

```javascript
db.movies.find({
  rated: {
    $in: ["PG", "PG-13"],
  },
});
```

- A compound query can specify conditions for more than one field in the collection's documents. Implicitly, a logical AND conjunction connects the clauses of a compound query so that the query selects the documents in the collection that match all the conditions.

```javascript
db.movies.find({
  countries: "Mexico",
  imdb.rating: {
    $gte: 7
    }
  })
```

---

### Update

[Back to summary](#mongodb)

To update a document, MongoDB provides [update operators](https://docs.mongodb.com/manual/reference/operator/update/), such as $set, to modify field values.

- Use the db.collection.updateOne() method to update the first document that matches a specified filter.

```javascript
db.movies.updateOne( { title: "Tag" },
{
  $set: {
    plot: "One month every year, five highly competitive friends \
    hit the ground running for a no-holds-barred game of tag"
  }
  { $currentDate: { lastUpdated: true } }
})
```

- Use the db.collection.updateMany() to update all documents that match a specified filter.

```javascript
db.listingsAndReviews.updateMany(
  { security_deposit: { $lt: 100 } },
  {
    $set: { security_deposit: 100, minimum_nights: 1 },
  }
);
```

-To replace the entire content of a document except for the \_id field, pass an entirely new document as the second argument to db.collection.replaceOne(). When replacing a document, the replacement document must contain only field/value pairs. Do not include update operators expressions. The replacement document can have different fields from the original document. In the replacement document, you can omit the \_id field since the \_id field is immutable; however, if you do include the \_id field, it must have the same value as the current value.

```javascript
db.accounts.replaceOne(
  { account_id: 371138 },
  { account_id: 893421, limit: 5000, products: ["Investment", "Brokerage"] }
);
```

---

### Delete

[Back to summary](#mongodb)

- To delete all documents from a collection, pass an empty filter document {} to the db.collection.deleteMany() method.

```javascript
db.movies.deleteMany({});
```

- You can specify criteria, or filters, that identify the documents to delete. The filters use the same syntax as read operations.

```javascript
db.movies.deleteMany({ title: "Titanic" });
```

- To delete at most a single document that matches a specified filter (even though multiple documents may match the specified filter) use the db.collection.deleteOne() method.

```javascript
db.movies.deleteOne({ cast: "Brad Pitt" });
```

---

### Mongoose

[Back to summary](#mongodb)

- [Terminologies](#terminologies)
- [Schemas](#schemas)
- [Models](#models)
- [Data Validation](#data-validation)
- [Fetch Record](#fetch-record)
- [Update Record](#update-record)
- [Delete Record](#delete-record)
- [Helpers](#helpers)

---

#### Terminologies

---

[Back to summary](#mongoose)

##### Collections

‘Collections’ in Mongo are equivalent to tables in relational databases. They can hold multiple JSON documents.

##### Documents

‘Documents’ are equivalent to records or rows of data in SQL. While a SQL row can reference data in other tables, Mongo documents usually combine that in a document.

##### Fields

‘Fields’ or attributes are similar to columns in a SQL table.

##### Schema

While Mongo is schema-less, SQL defines a schema via the table definition. A Mongoose ‘schema’ is a document data structure (or shape of the document) that is enforced via the application layer.

##### Model

‘Models’ are higher-order constructors that take a schema and create an instance of a document equivalent to records in a relational database.

---

##### Schemas

---

[Back to summary](#mongoose)

Everything in Mongoose starts with a Schema. Each schema maps to a MongoDB collection and defines the shape of the documents within that collection.  
Each key in our code blogSchema defines a property in our documents which will be cast to its associated [SchemaType](https://mongoosejs.com/docs/schematypes.html).

```javascript
import mongoose from "mongoose";
const { Schema } = mongoose;

mongoose.connect("mongodb://localhost:27017/booksDB"); // Connect to booksDB and use it.
// Create it if inexistant

const blogSchema = new Schema({
  title: String, // String is shorthand for {type: String}
  author: String,
  body: String,
  comments: [{ body: String, date: Date }],
  date: { type: Date, default: Date.now },
  hidden: Boolean,
  meta: {
    votes: Number,
    favs: Number,
  },
});

// It's good practice to close connection to db when uneeded
mongoose.connection.close().then(() => {
  console.log("\nDisconnect...");
});
```

To use our schema definition, we need to convert our blogSchema into a Model we can work with. To do so, we pass it into mongoose.model(modelName, schema)

```javascript
const Blog = mongoose.model("Blog", blogSchema);
// ready to go!
```

By default, Mongoose adds an \_id property to your schemas.

```javascript
const schema = new Schema();

schema.path("_id"); // ObjectId { ... }
```

---

#### Models

---

[Back to summary](#mongoose)

Mongoose Schema vs. Model:

- A Mongoose model is a wrapper on the Mongoose schema. A Mongoose schema defines the structure of the document, default values, validators, etc., whereas a Mongoose model provides an interface to the database for creating, querying, updating, deleting records, etc.

```javascript
// Defining Model
MyModel = mongoose.model('ModelsName', modelSchema)

// Create Instance
let myInstance = new MyModel({
 field: "value"
})

myInstance.save()
   .then(doc => {
     console.log(doc)
   })
   .catch(err => {
     console.error(err)
   })

/*
{
  _id: 5a78fe3e2f44ba8f85a2409a, -> The _id field is auto-generated by Mongo and is a primary key of the collection.
          Its value is a unique identifier for the document.
  field: "value", -> The value of the field is returned
  __v: 0 -> __v is the versionKey property set on each document when first created by Mongoose.
       Its value contains the internal revision of the document.
}
*/
```

---

#### Data Validation

---

[Back to summary](#mongoose)

When creating your schemas, you can specify [validation rules](https://mongoosejs.com/docs/validation.html).  
Each field type can have the required validator.  
If validation doesn't pass, it will raise a ValidationError and give you details of that failure.

```javascript
const mongoose = require("mongoose");

const exempleSchema = new mongoose.Schema({
  firstField: String,
  FieldWithValidation: {
    // Mongoose will check if the value is a number between 1 and 10
    type: Number,
    min: 1,
    max: 10,
    // We define here that FieldWithValidation field is required
    // If we don't provide this field, it will raise an error when we attempt to save the document
    required: true,
  },
});
```

---

#### Fetch Record

---

[Back to summary](#mongoose)

Use find() method to fetch record

```javascript
MyModel.find({
  field: "value", // search query
})
  .then((doc) => {
    console.log(doc);
  })
  .catch((err) => {
    console.error(err);
  });
```

---

#### Update Record

---

[Back to summary](#mongoose)

Use findOneAndUpdate() method to update a single record.  
For performance reasons, Mongoose won’t return the updated document so we need to pass an additional parameter to ask for it

```javascript
MyModel.findOneAndUpdate(
  {
    field: "value", // search query
  },
  {
    field: "new value", // field:values to update
  },
  {
    new: true, // return updated doc
    runValidators: true, // validate before update
  }
)
  .then((doc) => {
    console.log(doc);
  })
  .catch((err) => {
    console.error(err);
  });
```

---

#### Delete Record

---

[Back to summary](#mongoose)

Use the findOneAndRemove call to delete a record. It returns the original document that was removed

```javascript
MyModel.findOneAndRemove({
  field: "value",
})
  .then((response) => {
    console.log(response);
  })
  .catch((err) => {
    console.error(err);
  });
```

---

#### Helpers

---

[Back to summary](#mongoose)

- Virtual Property  
  A virtual property is not persisted to the database. We can add it to our schema as a helper to get and set values.

```javascript
let mongoose = require("mongoose");

let userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String,
});

module.exports = mongoose.model("User", userSchema);

/*
Let’s create a virtual property called fullName which can be used to set values on 
firstName and lastName and retrieve them as a combined value when read:
*/
userSchema.virtual("fullName").get(function () {
  return this.firstName + " " + this.lastName; // Now we can get full name from firstname and lastname
});

userSchema.virtual("fullName").set(function (name) {
  let str = name.split(" ");

  // Now we can set fistName and lastName from fullname:
  // model.fullName = 'Thomas Anderson'
  this.firstName = str[0];
  this.lastName = str[1];
});
```

- Instance Methods  
  We can create custom helper methods on the schema and access them via the model instance

```javascript
userSchema.methods.getInitials = function () {
  // Returns the initials for the current user
  return this.firstName[0] + this.lastName[0];
};

// This method will be accessible via a model instance
let model = new UserModel({
  firstName: "Thomas",
  lastName: "Anderson",
});

let initials = model.getInitials();

console.log(initials); // This will output: TA
```

- Static Methods  
  Similar to instance methods, we can create static methods on the schema. Let’s create a method to retrieve all users in the database

```javascript
userSchema.statics.getUsers = function () {
  return new Promise((resolve, reject) => {
    this.find((err, docs) => {
      if (err) {
        console.error(err);
        return reject(err);
      }

      resolve(docs);
    });
  });
};

// Calling getUsers on the Model class will return all the users in the database
UserModel.getUsers()
  .then((docs) => {
    console.log(docs);
  })
  .catch((err) => {
    console.error(err);
  });
```

- Middleware  
  Middleware are functions that run at specific stages of a pipeline. Mongoose supports middleware for the following operations - Aggregate - Document - Model - Query
  For instance, models have pre and post functions that take two parameters - Type of event (‘init’, ‘validate’, ‘save’, ‘remove’) - A callback that is executed with "this" referencing the model instance
  Let’s add two fields called createdAt and updatedAt to our userSchema

```javascript
let mongoose = require("mongoose");

let userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String,
  createdAt: Date,
  updatedAt: Date,
});

module.exports = mongoose.model("User", userSchema);
```

When model.save() is called, there is a pre(‘save’, …) and post(‘save’, …) event that is triggered.  
For the second parameter, you can pass a function that is called when the event is triggered.  
These functions take a parameter to the next function in the middleware chain.
Let’s add a pre-save hook and set values for createdAt and updatedAt

```javascript
userSchema.pre("save", function (next) {
  let now = Date.now();

  this.updatedAt = now;
  // Set a value for createdAt only if it is null
  if (!this.createdAt) {
    this.createdAt = now;
  }

  // Call the next function in the pre-save chain
  next();
});
```

Let’s create and save our model

```javascript
let UserModel = require('./user')

let model = new UserModel({
  fullName: 'Thomas Anderson'
}

msg.save()
   .then(doc => {
     console.log(doc)
   })
   .catch(err => {
     console.error(err)
   })
/*
{ _id: 5a7bbbeebc3b49cb919da675,
  firstName: 'Thomas',
  lastName: 'Anderson',
  updatedAt: 2018-02-08T02:54:38.888Z,
  createdAt: 2018-02-08T02:54:38.888Z,
  __v: 0 }
*/
```

- Plugins  
  Suppose that we want to track when a record was created and last updated on every collection in our database.  
  Instead of repeating the above process, we can create a plugin and apply it to every schema.  
  Let’s create a plugin

```javascript
module.exports = function timestamp(schema) {

  // Add the two fields to the schema
  schema.add({
    createdAt: Date,
    updatedAt: Date
  })
```

To use this plugin, we simply pass it to the schemas that should be given this functionality

```javascript
let timestampPlugin = require("./plugins/timestamp");

emailSchema.plugin(timestampPlugin);
userSchema.plugin(timestampPlugin);
```

- Query Building  
  There are lots of [Queries](https://mongoosejs.com/docs/api/query.html) we can use in mongoose.  
  Here is an example

```javascript
UserModel.find()                   // find all users
         .skip(100)                // skip the first 100 items
         .limit(10)                // limit to 10 items
         .sort({firstName: 1})      // sort ascending by firstName
         .select({firstName: true} // select firstName only
         .exec()                   // execute the query
         .then(docs => {
            console.log(docs)
          })
         .catch(err => {
            console.error(err)
          })
```

--- Work In Progress ---
