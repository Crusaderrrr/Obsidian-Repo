---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
  - React_JS
note type: Informational Note
---
We have some state that is relevant to the page we are on. 
If we want some elements to appear or be present in any form on multiple pages we need to use React context. 
> [!info] A context will allow state to be globally available to anything that's within the provided content.

Create a `context` folder and a file `MovieContext.jsx`:
```jsx
import { createContext, useState, useContext, useEffect } from "react";
  
const MovieContext = createContext()
  
export const useMovieContext = () => useContext(MovieContext)
  
export const MovieProvider = ({children}) => {
    const [favorites, setFavorites] = useState([]);
  
    useEffect(() => {                                      // working with local storage
        try {
            const storedFavs = localStorage.getItem("favorites");
            if (storedFavs) 
                setFavorites(JSON.parse(storedFavs));
            }
        } catch (error) {
           console.error("Error parsing favorites from localStorage:", error);
            localStorage.removeItem("favorites"); // Clear invalid data
        }
    }, [])
  
    useEffect(() => {
        localStorage.setItem('favorites', JSON.stringify(favorites))
    }, [favorites])
  
    const addToFavorites = (movie) => {
        setFavorites(prev => [...prev, movie])
    }
  
    const removeFromFavorites = (movieId) => {
        setFavorites(prev => prev.filter(movie => movie.id !== movieId))
    }
  
    const isFavorite = (movieId) => {
        return favorites.some(movie => movie.id === movieId)
    }
  
    const value = 
        favorites,
        addToFavorites,
        removeFromFavorites,
        isFavorite
    }
  
    return <MovieContext.Provider value={value}>
        {children}
    </MovieContext.Provider>
}
```