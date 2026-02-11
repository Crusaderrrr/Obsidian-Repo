---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
  - mongodb
note type: Informational Note
---
Link to the Transactions Tutorial: [click](https://www.mongodb.com/docs/manual/core/transactions/)

**Options of setting up Transactions**:
- *Single Node replica set on Local MongoDB server*
- *Replica Sets with MongoDB Atlas* 
	- ideal for production
	- cloud based 
	- fully managed

We will use the second one

Also, we need to install the `mongo shell` as it is not built-in. 
Set a new environment variable in system's PATH.
Run the `mongosh` command in command line (windows shell)

Now we need to create a **new project** in MongoDB Atlas:
- *password*: tP9GwCG5jZojsOcf 
- *username*: admin

Then we go to **network access**:
- add my IP address 
- add access from anywhere

Go back to **clusters**:
- *Connect*
- copy the command: `mongodb+srv://admin:<db_password>@farewheels.jn9lcej.mongodb.net/?retryWrites=true&w=majority&appName=FareWheels` replacing the *<db_password>* with our password.
- change the `index.js` file
```JavaScript
mongoose.connect('mongodb+srv://admin:<db_password>@farewheels.jn9lcej.mongodb.net/FareWheels?retryWrites=true&w=majority&appName=FareWheels')
```
- add a name of the company after `.net/` to create a database

**And MongoDB Atlas is ready to use!**

### Using 
we need to change some things, for example in the `post` route:
```JavaScript
router.post('/', async (req, res) => {
const session = await mongoose.startSession()
session.startTransaction();

  try {
  const { error } = validate(req.body);
  if (error) return res.status(400).send(error.details[0].message)
  const car = await Car.findById(req.body.carId);
  if (!car) return res.status(400).send('The Car with the given ID was not found');
  
  if (car.numberInStock === 0) return res.status(400).send('This car is out of stock at the moment.') 

  const customer = await Customer.findById(req.body.customerId);
  if (!customer) return res.status(400).send('The Customer with the given ID was not found');

  let rental = new Rental({
    car: {
      _id: car._id,
      modelName: car.modelName,
      dailyRentalRate: car.dailyRentalRate
    },
    customer: {
      _id: customer._id,
      name: customer.name,
      phone: customer.phone
    }
  })
  rental = await rental.save({session}); // passing object that is used in transactions

  car.numberInStock--;
  await car.save({session})
  
  await session.commitTransaction(); // perform changes
  session.endSession();

  res.send(rental);
} catch (err) {
  await session.abortTransaction();
  await session.endSession();
  res.send.status(500).send('Your vehicle is not booked. Something went wrong')
}
});
```

