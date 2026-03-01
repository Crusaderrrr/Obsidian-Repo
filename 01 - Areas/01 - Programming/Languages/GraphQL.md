This is a complete **Query Language**.

## The Problem
By querying DB we can retrieve more data that we wanted (nested tables, etc.), to solve this issue we would need to create many endpoints or something similar. 

*Classical approach*:
- server defines the scheme and a format of the returned data

*GraphQL approach*:
- Server defines only scheme, and client request necessary data

## Some concepts
- `QUERY` - analogy of GET request
- `MUTATION` - analogy of POST request
- `SUBSCRIPTION` - real time (built over websockets)

## Usage

1. We normally define the data:
```sql
type Query {
	hero: Character
}
```

2. Then we retrieve data:
```json
{
	hero {
		name
	}
}
// name is returned like that:
{
	"data": {
		"hero"{
			"name": "Hero Name"
		}
	}
}
```

# Advantages 
We use less traffic, meaning that we can use less resources to manipulate data between server and client.