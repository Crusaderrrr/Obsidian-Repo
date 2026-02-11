#JavaScript
#### Основные методы:
`array.push` добавить элемент в конец
`array.pop` удалить последний элемент и присвоить это значение переменной 
`array.unshift` новый элемент в начало массива
`array.shift` удалить первый элемент

### forEach()
```JS
array.forEach((element, index) => {
console.log(element, index)
})

// element1, 0
// element2, 1
// element3, 2
```
- не изменяет исходный массив
- возвращает undefined
```JS
array.map(el => el * 3)
// как map в pyhton
```

### map, reduce, filter:
```JavaScript
const numbers = [1, 2, 3, 4];

// map: Transform each element
const doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8]

// filter: Keep elements that meet a condition
const evens = numbers.filter(num => num % 2 === 0);
console.log(evens); // [2, 4]

// reduce: Sum all elements
const sum = numbers.reduce((total, num) => total + num, 0);
console.log(sum); // 10

// forEach: Log each element
numbers.forEach(num => console.log(num)); // 1, 2, 3, 4
```

It works quite like in Python
- All the methods require *function as an argument* (can be arrow function)
	`arary.map(elem => elem * 2)`
- **Map** create a new array