#JavaScript 

```JS
const myDict = {
    elem: 'darova',
    poshel_nahuy: function () {
        console.log('Иди нахуй!')
    }
}
```

это тоже самое, что:

```JS
const myDict = {
    elem: 'darova',
    poshel_nahuy() {
        console.log('Иди нахуй!')
    }
}
```


**Object distribution**:
```JavaScript
person = {
	name: 'Nikita',
	age: 19,
	isMaried: false, 
};

const {name, age, isMaried} = person
console.log(`My name is ${name}, I'm ${age} years old, and I'm ${isMaried}`) //My name is Nikita, I'm 19 years old, and I'm false
```
