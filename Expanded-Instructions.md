## Expanded Instructions  

1) Project Setup
- Create a new github repository called react-movie-app and add the link to populi
- Clone the repository and initialize it by running 'npx create-react-app .' inside the project directory and running 'npm i react-router-dom' to install react router.
- Open App.js and replace the initial code with the following code:
```
import "./App.css";

const App = () => {
	return (
		<div className="App-header">

		</div>
	);
}

export default App;
```
- In the ./src folder, create three new folders:
	- ./src/Components
	- ./src/Layouts
	- ./src/Pages
	- _Note_: These folders are going to house the react components we create for our application from now on. You do not need to strictly adhere to this folder structure for future projects, but rather treat it as a basic guideline for how to organize your project files.

2) Creating the Base Nav Layout and Home Page
- Create three new files
	- ./src/Components/NavBar.js
	- ./src/Layouts/NavLayout.js
	- ./src/Pages/HomePage.js
- In ./src/Components/NavBar.js, 
	- Create a new react component ```<NavBar/>``` and default export it from the file. 
	- Set the class of the enclosing ```<divs>```'s in ```<NavBar/>``` to be the class "nav-bar". [1]
- In ./src/Layouts/NavLayout.js
	- Create a new react component ```<NavLayout/>``` and default export it from the file.
	- Set the class of the enclosing ```<div>```'s in <NavLayout/> to be "nav-layout"
	- Import NavBar from "../Components/NavBar" and add an instance of the ```<NavBar/>``` component to the JSX of ```<NavLayout/>```
	- Import { Outlet } from 'react-router-dom' and add it to the JSX of ```<NavLayout/>``` below the ```<NavBar/>```. [2]
- In ./src/Pages/HomePage.js,
	- Create a new react component ```<HomePage/>``` and default export it from the file.
	- Add an h1 header that says Home Page in the JSX of ```<HomePage/>```

3) Creating the Base Application Routes
- _Approach_: Now that we have created our basic ```<NavLayout/>``` that contains our navigation bar as well as our basic ```<HomePage/>```, we are going to create a Browser Router from react-router to configure our basic routes. 
- _Note_: 
	- Normally in react-router applications, the Browser Router would go in the index.js file since that is a react-router best practice. However, this makes storing and passing around top level application state difficult (such as our eventual movieList variable). If this were a real world production application, we would implement some sort of global state management library such as Redux to handle our application state (as you will do in term 3). 
	- In order to keep things simple for now however, we are going to put the Browser Router inside of ```<App/>``` instead of index.js. This way we can use the state of the ```<App/>``` component as our "global" state variable store and simply pass those state variables down as props to our various route elements/components so that we can use them across our application. 
- In ./src/App.js,
	- import { createBrowserRouter, RouterProvider } from "react-router-dom".
	- In the body (above the JSX) of ```<App/>``` create a new variable named router that is set to createBrowserRouter with an empty array as its argument to create a new Browser Router. [3]
	- Create a new the top level route in the browserRouter by adding an object to the routes array that has the path property set to "/" and the element property set to ```<NavLayout/>```. 
	- Create a new child route of the "/" route object using the children property that has the index property set to true and the element set to <HomePage/> [4]
	- In the JSX of ```<App/>```, add a new instance of ```<RouterProvider/>``` and pass in router as a prop. [5]
	- _Commentary_: By creating the topmost route of "/" to be the ```<NavLayout/>``` element, we are going to render ```<NavLayout/>``` to the page for all of our routes. We set ```<HomePage/>``` to be the index route of "/" so that the <HomePage/> element will display to the page when we visit localhost:3000/. The JSX of ```<HomePage/>``` will render inside of the JSX of ```<NavLayout/>``` since we included the ```<Outlet/>``` component in ```<NavLayout/>```. In this way, we can ensure that the ```<NavBar/>``` displays for every page in our application without having to include it in every file.
- In ./src/Components/NavBar,
	- Add a new ```<Link/>``` to the JSX of ```<NavBar/>```that links to "/" with the display text of 'Home'. 
- If you implemented the above correctly, you should be able to visit localhost:3000/ and see the Home Page and NavBar render. Additionally, inspect the page elements with chrome dev tools to verify that the Home Page elements are rendering within the Nav Layout. 

4) Creating the Movie Layout, Movie Sidebar and Movie List Page
- _Approach_: Now that we have our base application setup, we are going to start building our the movies section of our application. The movie layout will provide a framework to display our movie list as well as a list of movie links in the sidebar. It will also allow us to style our movie pages in such a way that we will not have to repeat css for multiple pages.
- Create three new files
	- ./src/Layouts/MovieLayout.js
	- ./src/Components/MovieSidebar.js
	- ./src/Pages/MovieListPage.js
- In ./src/Components/MovieSidebar.js,
	- Create a new react component ```<MovieSidebar/>``` and default export it from the file.
	- Set the class of the enclosing ```<div>```'s in ```<MovieSidebar/>``` to be "movie-sidebar"
	- Add an h2 header that says "Movie Sidebar" to the JSX of ```<MovieSidebar/>```.
- In ./src/Pages/MovieListPage.js,
	- Create a new react component ```<MovieListPage/>``` and default export it from the file.
	- Add an h1 header that says "Movie List Page" to the JSX of ```<MovieListPage/>```.
- In ./src/Layouts/MovieLayout.js,
	- Create a new react component ```<MovieLayout/>``` and default export it from the file.
	- Set the class of the enclosing ```<div>```'s in ```<MovieLayout/>``` to be "movie-layout"
	- Import MovieSideBar from "../Components/MovieSideBar" and add an instance of ```<MovieSideBar/>``` to the JSX of ```<MovieLayout/>```
	- Add a ```<div>``` with the class of "movie-content" below ```<MovieSideBar/>```
	- import { Outlet } from "react-router-dom" and within the "movie-content" ```<div>``` you just created, add an instance of ```<Outlet/>``` [6]
- In ./src/App.js,
	- Add a new path to the router as a child of "/" with the path "/movies" and the element of ```<MovieLayout/>```
	- Add a new path to the router as a child of "/movies" set to be the index route with the element of ```<MovieListPage/>``` [7]
- In ./src/Components/NavBar,
	- Add a new ```<Link/>``` to the JSX of ```<NavBar/>``` that links to "/movies" with the display text of 'Movie List'. 

5) Building Out Movie Layout and Movie Sidebar
- In ./src/App.js,
	- Copy/paste the JSON data from this github gist into a new variable sampleMovies in the global scope:
		- https://gist.github.com/saniyusuf/406b843afdfb9c6a86e25753fe2761f4
	- In the body of ```<App/>```, add a new state variable movieList that is initialized to sampleMovies. [8]
	- In the routes list, pass movieList as a prop into ```<MovieLayout/>``` and ```<MovieListPage/>```. [9]
- In ./src/MovieLayout.js,
	- Pass movieList from the ```<MovieLayout/>``` props into  ```<MovieSideBar/>``` as a prop. [10]
- In ./src/MovieSideBar.js,
	- Map through the movieList prop in the JSX of ```<MovieSideBar/>``` below the h2 header and return a ```<Link>``` component for every movie in the list. The displayed text of the ```<Link/>``` should be the movie title and the to prop should be the calculated path of /movies/{movie title} [11]
	- If the above was implemented properly, you should see a screen that looks like Screen Shot 1.
- In ./src/App.css,
	- Change the css property justify-content: center; in the .App-header class to be justify-content: flex-start; instead.
	- Add css to the .nav-layout, .nav-bar, .movie-layout, .movie-sidebar and .movie-content classes to make the page look like Screen Shot 2. 
		- The styling does not need to exactly match. The important parts are that:
			- nav-layout displays as a flex column
			- movie-layout displays as a flex row
			- movie-sidebar displays as a flex column
			- movie-content takes two thirds of the space in movie-layout and movie-sidebar takes up one third of the space
		- _Suggestion_: Add the following class to see the links more easily
			- a {
				color: white;
			}
	- See the ## Final CSS section for the full list of new css classes.

6) Building Out the Movie List Page
- Create a new file ./src/Components/MovieCard.js
- In ./src/Components/MovieCard.js,
	- Create a new react component ```<MovieCard/>``` and default export it from the file.
	- Set the class of the enclosing ```<div>```'s in ```<MovieCard/>``` to be "movie-list-card"
- In ./src/Pages/MovieListPage,
	- Add a new ```<div>``` below the h1 header with the class "movie-list"
	- Inside the "movie-list" ```<div>```, map through movieList coming from the props in the JSX of ```<MovieListPage/>``` and return a ```<MovieCard/>``` component for every movie with the movie data passed into ```<MovieCard/>``` as a prop. [12]
- In the JSX of ```<MovieCard/>```,
	- Display the movie title in an h2 header tag
	- Display the movie director in a p tag
- In ./src/App.css,
	- Add css to movie-list-card that provides a white border, margin and padding to ```<MovieCard/>```.
	- Add css to movie-list that sets the maximum height to 80vh and the y-axis overflow to scroll.
- If you implemented the above properly, you should now have a display that looks like Screen Shot 3. The movie list should also be vertically scrollable.

7) Creating the Movie Page
- _Approach_: Now that we have the movie list displaying, we also want to create an expanded view for just a single movie. We are going to find the particular movie to display by getting the title param from the props which will be automatically generated for us with the links in the movie sidebar, looping through the movie list and displaying the movie that matches the title prop onto the movie page. 
- Create a new file ./src/Pages/MoviePage.js 
- In ./src/Pages/MoviePage.js,
	- Create a new react component ```<MoviePage/>``` and default export it from the file.
	- Add an h1 header that says Movie Page in the JSX of ```<MoviePage/>```
- In ./src/App.js,
	- Add a new path to the router as a child of "/movies" with the path ":title" and the element of ```<MoviePage/>```. Pass movieList as a prop into ```<MoviePage/>```. [13]
- In ./src/Pages/MoviePage.js,
	import { useParams } from "react-router-dom";
	- Get the url title param from the url using the useParams react-router hook. [14]
	- Loop through movieList coming from props and find the movie whose Title property matches the title param in the url. 
		- _Hint_: Click on one of the links in the movie sidebar, that will render the Movie Page so you can console.log the above code to verify that it's working while you develop the code.
	- In the JSX of ```<MoviePage/>```, display the found movie title in an h2 header, and the director, actors and plot in p tags.
- If you implemented the above correctly, you should be able to click any one of the links in the movie sidebar, see the url change in the browser address bar and see a display that looks like screenshot 4.

8) Creating the Movie Form Page
- Create a new file ./src/Pages/MovieFormPage.js 
- In ./src/Pages/MovieFormPage.js,
	- Create a new react component ```<MovieFormPage/>``` and default export it from the file.
	- Add an h1 header that says Movie Form Page in the JSX of ```<MovieFormPage/>```
- In ./src/App.js,
	- In the body of <App/> create a new function (above the router) called handleAddMovie that takes in title as its parameter. The function handleAddMovie should create a new movie object using the title parameter and add it to the movieList state variable. [15]
		- _Note_: 
			- We're only implementing title for now, but one of the stretch goals is to build out the full form. 
			- Make sure you pay attention to the casing on the currently existing movie objects in sampleMovies and match the case for your new movie object.
	- Add a new path to the router as a child of "/movies" with the path "form" and the element of ```<MovieFormPage/>```. Pass handleAddMovie as a prop into ```<MoviePage/>```.
- In ./src/Components/NavBar,
	- Add a new ```<Link/>``` to the JSX of ```<NavBar/>``` that links to "/movies/form" with the display text of 'Movie Form'. 
- In ./src/Pages/MovieFormPage.js,
	- Add a state variable, a ```<label>``` and text ```<input>``` field to save the title user input.
	- Add a button with the display text of 'Add Movie' that calls handleAddMovie with the title passed in as a argument onClick. [17]
- If you implemented the above correctly, you should be able to:
	- Enter a new title into the Movie Form and click Add Movie.
	- See the movie appear on both the movies sidebar as well as the movie list page.
	- Click on one of the movies sidebar links and see the movie page for your new movie.

**********STRETCH_GOALS**********

1) Build out ```<MovieForm/>``` to be able to handle all inputs necessary to create a movie object with all the movie fields.
2) Build out ```<MoviePage/>``` to display all the movie object data.
3) Build out ```<MovieCard/>``` to display a few more movie fields without making the card too large such as an image on the left side of the card, the genre, release date, etc.
4) Experiment with additional css styles (or even twitter bootstrap styles) to build out the UI of the application.
