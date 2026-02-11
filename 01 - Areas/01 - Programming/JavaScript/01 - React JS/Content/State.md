---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
  - React_JS
note type: Informational Note
---
So, here we have a home page:
```jsx
import MovieCard from "../components/MovieCard"
import {useState} from "react"

function Home() {
    const [searchQuery, setSearchQuery] = useState("");  

    const movies = [
        {id: 1, title: "John Wick", release_date: '2020'},
        {id: 2, title: "Terminator", release_date: '1999'},
        {id: 3, title: "Matrix", release_date: '1998'},
    ]

    const handleSearch = (e) => {
        e.preventDefault()
        alert(searchQuery)
        setSearchQuery('---------')
    }

    return <div className="home">
        <form onSubmit={handleSearch} className="search-form">
            <input
            type="text"
            placeholder="Search for movies..."
            className="search-input"
            value={searchQuery}
            onChange={(e) => setSearchQuery(e.target.value)}
            />
            <button type="submit" className="search-button">Search</button>
        </form>

       <div className="movies-grid">
            {movies.map(
                movie =>
                    movie.title.toLowerCase().startsWith(searchQuery) && (
                    <MovieCard movie={movie} key={movie.id}/>
        ))}
        </div>
    </div>
};

export default Home
```

Description:
- The `handleSearch()` function handles a search form's behavior. It uses three methods:
	- `e.preventDefault` - prevents a default behavior (refreshing the search form after search)
	- `alert(searchQuery)` - will appear an alert after searching with the message we have put in the search form
	- `setSearcQuery('-----')` - after searching the '----' will appear in the search form. 
- `movies.map(..)` is used to run a specific function with every movie we have
	- This function is used to find a movie, when we type anything in a search form, and it re-renders the page with every sign typed 