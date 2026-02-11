---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - mongodb
  - JavaScript
note type: Informational Note
---
This is a NoSQL data base. 
It is way more complex than we are gonna see it in this course.

**Starting work with MongoDB**:
- Firstly we need to install it from the site
- Then we need to create a environment variable in our **advanced system settings**
- Then we create a folder for MongoDB
- Initiate in in terminal with `monogd` command
- Create a new `mongo-demo` folder and run `npm init --yes` 
- Create a new `index.js` file 
- Install `mongoose` module with `npm i` and import it to the `index.js` file
- Run the file and make sure everything works

*Code*:
```JavaScript
const mongoose = require('mongoose');

mongoose.connect('mongodb://127.0.0.1:27017/playground') // Returns Promise
.then(() => console.log("Connected to MongoDB"))
.catch(err => console.error("Connection to MongoDB failed...", err))
```

### Creating a Schema
It is a *mongoose* specific concept
```JavaScript
const courseSchema = new mongoose.Schema({
    name: String,
    author: String,
    tags: [ String ],
    date: { type: Date, default: Date.now },
    isPublished: Boolean
});
```

Here we define the schema, that gives a shape of documents in MongoDB collection.
In the code above:
- we define schema that:
	- specifies the name property to be a string 
	- autor too
	- tags is gonna be an array of string 
	- date is gonna have type date and we won't need to specify it when creating a course
	- isPublished - true or false

**Types we can use in schema**:
- String
- Number 
- Date
- ObjectID
- Buffer
- Array
- Boolean

### Creating an instance with schema 
```javascript
const Course = mongoose.model('Course', courseSchema); // Uppercase means that this is a class
const course = new Course({
    name: "The Express.js Course",
    author: "Shiven",
    tags: ["express", "backend"]
    isPublished: true
});
```
Here the Course class is getting created with the help of the schema, and then I create an instance of a class with `new Course()`.

### Creating a Query (filtering)
```javascript
const getCourses = async () => {
    const courses = await Course
    .find({ author: "Shiven", isPublished: true})
    .limit(10)
    .sort({ name: -1})
    .select({ name: 1, tags: 1})
    console.log(courses);
};
```
That's a complex query. 
- finds a course with a specific properties 
- applies a limit
- sorts document by the names in ascending order (1)
- we get only name and tags properties ascending name and descending tags

**IMPORTANT**
`.select()` values can be string with spaces, like `'name, author, price'`

**Comparison operators**:
- eq - Equal
- ne - Not Equal
- gt - Greater than
- gte - Greater Than or Equal to 
- lt - Less Than
- lte - Less Than or Equal to
- in
- nin - Not IN

In the code above we can do the next thing:
```javascript
const getCourses = async () => {
	const courses = await Course
	.find({ prince: { $gte: 10, $lte: 20 } })
}
```
This code means that the course's price could be expressed with this: `10 <= price <= 20`

```javascript
    .find({ price: {$in: [10, 15, 20]} })
```
This means that the price can only be one of the values of this array.

**Logical operators**:
- or 
- and
```JavaScript
const getCourses = async () => {
    const courses = await Course
    .find()
    .or([ {author: 'Siven'}, {isPublished: true} ])
    .limit(10)
    .sort({ name: -1})
```
Firstly goes `.find()` method and the or / and 
The code above means that we are searching for a course with the author's name Shiven *OR* which is published.

**Harnessing Regular Expressions**:
```JavaScript
...
	.find({ author: /^Shiven/ })
```
this code means that we are searching for the course with the author that *starts on word Shiven* and is case sensitive. This is a Regular Expression syntax  `/^word/` 

```JavaScript
...
	.find({ author: /Raguvanshi$/i })
```
the author *ends with Raguwanshi*, if we add i after the second slash, this query will become case insensitive. 

```JavaScript
	.find({ author: /.*Shiv.*/i })
```
the author *contains Shiv* and is case insensitive


### Count
if we want just to know a number of documents with a specific properties we need to add:
```JavaScript
...
	.count()
```
to our query function.


```JavaScript
const pageNumber = 2
const pageSize = 10

    .limit(pageSize)
    .skip((pageNumber-1) * pageSize)
```

`.limit()` -  Limits the number of documents returned by the query to the value of pageSize
`.skip()`  - Skips a certain number of documents before returning the results.

### Updating a document 
Approach 1:
- findByID()
- Modify its properties 
- save()

Approach 2:
- update it directly
- optionally: get the updated document 

```JavaScript
const updateCourse = async id => {
    // Approach 1
    const course = Course.findById(id)
    if (!course) return;
    course.isPublished = true;
    course.author = "Another author"
    
   // Optional
    const result = await course.save()
    console.log(result)

    // Approach 2
    course.set({
        isPublished: true,
        author: "another author"
    })
};

updateCourse('6807c0bbb4ee4c0d4873a37c');
```
It will update a course with this ID: 6807c0bbb4ee4c0d4873a37c

There are a lot of update operators, that could be found on the MongoDB documentation page.
```JavaScript
const updateCourse = async id => {
    const result = await Course.updateOne({_id: id}, {
        $set: {
            author: "Shivendra",
            isPublished: false
        }
    }, { new: true}) // get updated document
    console.log(result)
};
```

### Removing a document
```JavaScript
const removeCourse = async id => {
    const result = await Course.deleteOne({_id: id})
    console.log(result)
};
```
Removes a course with a particular ID
The `{_id: id}` can be `{isPublished: true}` or any other property.

Also, there is a function:
```JavaScript
const removeCourse = async id => {
    const result = await Course.deleteMany({_id: id})
    console.log(result)
};
```

and if we want to find a deleted course by id:
```JavaScript
const removeCourse = async id => {
    const result = await Course.findByIDAndRemove({_id: id})
    console.log(result)
};
```
will return null if there is removed course with a particular ID.

# Importing other documents to DB
Use the command:
`mongoimport --db mongo-exercises --collection courses --drop --file exercise-data.json --jsonArray` need to be ran in the folder with .json file.


### Validating data 
```JavaScript
const createCourse = async () => {
    const course = new Course({
        name: "The Express.js Course",
        author: "Shiven",
        tags: ["react.js", "frontend"],
        isPublished: true
    });
    try {
       const result = await course.save(); // asynchronous operation (returns a Promise)
       console.log(result);
    } catch (err) {
        console.log(err.message);
    }
}
```
this is an enhanced function with try/catch block that validates whether the course can be posted or not, also:
```JavaScript
const courseSchema = new mongoose.Schema({
    name: { type: String, required:true },
    author: String,
    ...
```
This name property now is required.

#### Built-in Mongoose Validators
```JavaScript
const courseSchema = new mongoose.Schema({
    name: {
	    type: String,
	    required:true ,
	    minlength: 5,
	    maxlength: 255,
	    match: /pattern/
    },
    category: {
        type: String,
        enum: ['web', 'mobile', 'network'],
        required: true
    },
    author: String,
    price:{
        type: Number,
        min: 10,
        max: 20,
	    required: function() { return this.isPublished}},
    tags: [ String ],
    date: { type: Date, default: Date.now },
    isPublished: Boolean
});
```
- in the **name** property:
	- minlength and maxlength are logically understandable 
	- match is used in order to validate emails, phone numbers and things like that, which has a *pattern*
- **Category**
	- enum - is used to define an array of values that can be used by this property
- **Price**
	- min and max are logical too
	- required function means that if the course is published (this refers to a course object)
		- if *isPublished is true* - then price is *required*
		- for and oposite case it won't be required

### Creating a Custom Validator
```JavaScript
 tags: {
        type: Array
        validate: {
            validator: function(v) {
                return v && v.length > 0
            },
            message: "A course should have at least one tag!"
        }
    }
...
```
In this code we se a validate property that contains a function and a message, the function is type sensitive, by this I mean that if we try to pass null as and argument it won't work.
So, if the function returns false -> the message will appear.

### Handling Validation Errors
```JavaScript
const createCourse = async () => {
    const course = new Course({
        name: "The Express.js Course",
        author: "Shiven",
        tags: null,
        isPublished: true,
        price: 15,
        category: 'web'
    });
    
    try {
       const result = await course.save(); // asynchronous operation (returns a Promise)
       console.log(result);
    } catch (err) {
        for (field in err.errors) {
            console.log(err.errors[field].message)
        }
    }
}
```

This try/catch block now can handle errors and reveal a messages for every error that occurs.


### Additional Validators
```JavaScript
category: {
        type: String,
        enum: ['web', 'mobile', 'network'],
        required: true,
        lowercase: true,
        // uppercase: true,
        trim: true,
    },
```
There are more *String* validators:
- lowercase
- uppercase
- trim - removes all paddings

```JavaScript
    price:{
        type: Number,
        min: 10,
        max: 200,
        get: v => Math.round(v),
        set: v => Math.round(v),
        required: function() { return this.isPublished}},
```
- get - gets a round value of a price
- set - sets this rounded price