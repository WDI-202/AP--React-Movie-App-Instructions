## Code References
- [1]
```
const NavBar = () => {
	return (
		<div className="nav-bar">
		</div>
	)
}

export default NavBar;
```
- [2]
```
const NavLayout = () => {
	return (
		<div className="nav-layout">
			<NavBar/>
			<Outlet/>
		</div>
	)
}
```
- [3]
```
const router = createBrowserRouter([])
```
- [4]
```
const router = createBrowserRouter([
	{
		path: "/",
    element: <NavLayout />,
		children: [
			{
				index: true,
				element: <HomePage/>
			}
		]
	}
])
```
- [5]
```
const App = () => {
	return (
    <div className="App-header">
      <RouterProvider router={router} />
    </div>
  );
}
```
- [6]
```
<div className="movie-layout">
	<MovieSideBar />
	<div className="movie-content">
		<Outlet />
	</div>
</div>
```
- [7]
```
 {
	path: "/",
	element: <NavLayout />,
	children: [
		{
			index: true,
			element: <HomePage/>
		},
		{
			path: "/movies",
			element: <MovieLayout />,
			children: [
				{
					element: <MovieListPage />,
					index: true,
				},
			],
		},
	],
},
```
- [8]
```
const [movieList, setMovieList] = useState(sampleMovies);
```
- [9]
```
{
	path: "/movies",
	element: <MovieLayout movieList={movieList} />,
	children: [
		{
			element: <MovieListPage movieList={movieList} />,
			index: true,
		},
	],
},
```
- [10]
```
const MovieLayout = (props) => {
	const {movieList} = props;
  return (
    <div className="movie-layout">
      <MovieSideBar movieList={movieList}/>
      <div className="movie-content">
        <Outlet />
      </div>
    </div>
  );
};
```
- [11]
```
const MovieSideBar = (props) => {
	const {movieList} = props
	return (
		<div className="movie-sidebar">
			<h2>Movie Sidebar</h2>
			{props.movieList.map((movieItem)=>{
				return (
					<Link to={`/movies/${movieItem.Title}`}>{movieItem.Title}</Link>
				)
			})}
		</div>
	)
}
```
- [12]
```
<div>
	<h1>Movie List Page</h1>
	<div className="movie-list">
		{props.movieList.map((movie) => {
			return <MovieCard movie={movie} />;
		})}
	</div>
</div>
```
- [13]
```
{
	element: <MoviePage movieList={movieList}/>,
	path: ":title",
}
```
- [14]
```
const params = useParams()
const titleParam = params.title
```
- [15]
```
const handleAddMovie = (title) => {
	const newMovie = {
		Title: title
	}
	setMovieList([...movieList, newMovie])
}
```
- [16]
```
{
	element: <MovieFormPage handleAddMovie={handleAddMovie} />,
	path: "form",
}
```
- [17]
```
<button onClick={()=>{
	handleAddMovie(title)
}}>Add Movie</button>
```

## Final CSS

.nav-layout {
	width: 100%;
	display: flex;
	flex-direction: column;
	align-items: center;
}

.nav-bar {
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	width: 70%;
}

.movie-layout {
	display: flex;
	flex-direction: row;
	width: 100%;
	justify-content: space-between;
}

.movie-sidebar {
	flex: 1;
	display: flex;
	flex-direction: column;
	margin: 10px;
}

.movie-content {
	flex: 2;
}

a {
	color: white
}

.movie-list {
	overflow-y: scroll;
	max-height: 80vh;
}

.movie-list-card {
	border: 1px solid white;
	margin: 10px;
	padding: 20px;
} 
