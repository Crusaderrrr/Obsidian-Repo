#JavaScript 

```JS
try {
	блок кода
} catch (error) {
	блок кода, если ошибка в try
}
```

#### Пример:
```JS
try {
fnWithError()
} catch (error) {
console.error(error)
console.log(error.message)
}