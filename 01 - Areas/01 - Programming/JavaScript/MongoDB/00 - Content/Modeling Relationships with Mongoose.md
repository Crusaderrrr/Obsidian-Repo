---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - node_js
  - JavaScript
  - programming
  - mongodb
note type: Informational Note
---
### Approach Types
There are 3 approaches of storing data:
**Normalization**:
- by making references from one object to another.
- it is characterized by *consistency*. 
- but we would need to make *a lot of queries*. (slow)
```JavaScript
let author = {
	name: "Nikita"
};

let course = {
	author: 'id'
};
```

**Denormalization**:
- embedded documents 
- less queries 
- *performance* 
```JavaScript
let course2 = {
	author: {
		name: "Nikita",
		// other properties	
	}
};
```

**Hybrid**:
```JavaScript
let author2 = {
	name: "Nikita",
	// other properties (ex: 50)
};

let course3 = {
	author: {
		id: 'ref',
		name: 'Nikita'
	}
};
```

### Implementation 
**Normalization**
In the file with imported mongoose module:
```JavaScript
const mongoose = require("mongoose");
mongoose.connect("mongodb://127.0.0.1:27017/playground")
  .then(() => console.log("Connected to MongoDB..."))
  .catch((err) => console.error("Connection to MongoDB failed...", err));
  
const Author = mongoose.model('Author', new mongoose.Schema({
  name: String,
  bio: String,
  website: String
}));

const Course = mongoose.model('Course', new mongoose.Schema({
  name: String,
  author: {
    type: mongoose.Schema.Types.ObjectId,
    ref: "Author"
  }
}));

const createAuthor = async (name, bio, website) => {
  const author = new Author({
    name,
    bio,
    website
  })

  const result = await author.save();
  console.log(result);
}

const createCourse = async (name, author) => {
  const course = new Course({
    name,
    author
  });

  const result = await course.save();
  console.log(result);
}

const listCourses = async () => {
  const courses = await Course
    .find()
    .populate('author', 'name -_id')
    .select('name author');
  console.log(courses);
}

createAuthor('Shiven', 'About me', 'My website');

createCourse('Node Course', '680bb11b84ff885503fe9099');

listCourses();
```
- On lines 1-18 we set the models
- On lines 20-29 is the function that creates an author with particular properties like an ID
- On lines 31-39 is the similar function that creates a new course, but it will reference to the Author document using ObjectID. It creates a course linking it to an author with the author given ID.
- On lines 41-53 is the function that returns all the courses. It has next properties:
	- find 
	- `populate('author', 'name -_id')` that will give us only the *name of the author without his id*. We can call it multiple times 
- If author's id will be changed in a course object - there will be no errors, only **null** value of the author of the course.

**Denormalization**
*First approach*:
```JavaScript
const updateAuthor = async courseId => {
  const course = await Course.findById(courseId);
  course.author.name = "Nikita Bulash";
  course.save();
}
```

This function is changing the author's name if it is a subdocument of the course document:
![[Pasted image 20250425173406.png]]

*Second approach* (update directly):
```JavaScript
const updateAuthor = async courseId => {
  const course = await Course.updateOne({_id: courseId}, {
    $set: {
      'author.name': 'Peter Parker'
    }
  });
}
```
`$set` operator is used to update a specific object in MongoDB, if this object doesn't exist it will create it. Here we update and author's name in the subdocument of the course with the given id.

If we put `$unset` operator it will remove a property:
```JavaScript
...
$unset: {
	'author.name': ''
}
...
```

### Multiple Subdocuments 
*Firstly*, the course model and `createCourse()` function need to be modified:
```JavaScript
const Course = mongoose.model("Course", new mongoose.Schema({
    name: String,
    authors: [authorSchema] // now an array
  })
);
```

*Creating*: we now can create a course with multiple authors:
```JavaScript
createCourse("Express Course", [
	new Author({ name: "Shiven" }),
	new Author({name: "Peter"})
]);
```

*Adding*, we can define a new `addAuthor()` function:
```JavaScript
const addAuthor = async (courseId, author) => {
  const course = await Course.findById(courseId);
  course.authors.push(author);
  course.save();
};
```

*Removing* an author from a subdocument array:
```JavaScript
const removeAuthor = async (courseId, authorId) => {
  const course = await Course.findById(courseId);
  const author = course.authors.id(authorId);
  author.deleteOne();
  course.save();
};

removeAuthor('680bbc4de9daccff2a7f1406', '680bbc4de9daccff2a7f1404');
```
We need to know the courseId and authorId to remove it. 