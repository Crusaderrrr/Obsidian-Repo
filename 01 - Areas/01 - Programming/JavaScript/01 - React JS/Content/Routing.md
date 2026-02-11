---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - React_JS
  - JavaScript
note type: Informational Note
---
### Principal Routing

To enable routing with API endpoints we need to install a `npm i react-router-dom` module.
Then, we need to modify our `app.jsx` file:
```jsx
import './App.css'
import Favorites from './pages/Favorites';
import Home from './pages/Home'
import {Routes, Route} from 'react-router-dom'
  
function App() {
  
  const MovieNumber = 2;
  
  return (                          <!-- We are interested in this part-->
  <main className='main-content'>
    <Routes>
      <Route path='/' element={<Home />}/>
      <Route path='/favorites' element={<Favorites />}/>
    </Routes>
  </main>
  )
}
  
function Text({display}) {
  return (
    <div>
      <p>{display}</p>
    </div>
  )
}
  
export default App
```
When we are on the `/` page we will see a home page, if we navigate to the `/favorites` we will see our favorites page.

### NavBar
```jsx
  return (
  <div>
    <NavBar />
  <main className='main-content'>
    <Routes>
      <Route path='/' element={<Home />}/>
      <Route path='/favorites' element={<Favorites />}/>
    </Routes>
  </main>
  </div>
  )
}
```
we modify our App function and import a `NavBar` on the top:

```jsx
import { Link } from 'react-router-dom'
  
function NavBar () {
    return <nav className="navbar">
        <div className="navbar-brand">
            <Link to='/'>Movie App</Link>
        </div>
        <div className='navbar-links'>
            <Link to='/' className='nav-link'>Home</Link>
            <Link to='/favorites' className='nav-link'>Favorites</Link>
        </div>
    </nav>
}
  
export default NavBar;
```

### Fetching API
On the web: [click](https://www.themoviedb.org/)
We need to get the *API key*
Also, create a separate `services` folder with `api.js` file to handle api requests.
then we modify the home page code:
```jsx
function Home() {
    const [searchQuery, setSearchQuery] = useState("");
    const [movies, setMovies] = useState([]);
    const [error, setError] = useState(null);
    const [loading, setLoading] = useState(true);
  
    useEffect(() => {
        const loadPopularMovies = async () => {
            try {
                const popularMovies = await getPopularMovies()
                setMovies(popularMovies)
            } catch (err) {
                console.log(err)
                setError("Failed to load movies")
            }
            finally {
                setLoading(false)
            }
        }
  
        loadPopularMovies()
    }, [])
```
This allows us to fetch movies from a particular api and show them on the web page.

Also, to enable an access of React to the images of the movies we modify the `MovieCard.jsx`:
```jsx
return <div className="movie-card">
        <div className="movie-poster">
            <img src={`https://image.tmdb.org/t/p/w500${movie.poster_path}`} alt={movie.title}/>
            <div className="movie-title">
                <button className="favorite-btn" onClick={onFavoriteClick}>
                    ♡
                </button>
            </div>
        </div>
        <div className="movie-info">
            <h3>{movie.title}</h3>
            <p>{movie.release_date}</p>
        </div>
    </div>
```
On the 4'th line.