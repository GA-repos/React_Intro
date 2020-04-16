![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)

# Introduction to ReactJS

React was originally created by Facebook engineers in 2011 to improve the performance of its web app. Since its initial release as an open source project, React has become a dominant tool in the market for creating richly interactive web interfaces.  

## Learning Objectives

- Describe what ReactJS and what benefits it provides.
- Explain how and why component architectures are used in modern web applications.
- Create and render React components in the browser.

## Framing

Take 4 minutes to watch [What is React?](https://www.youtube.com/watch?v=N3AkSS5hXMA).

React was initially motivated by the need to improve the performance of complex, dynamic, data-rich, web application interfaces. At the same time, the engineers at Facebook were also looking to make their web app more easily maintainable, scalable, extensible and testable. There are 3 key aspects of React that evolved to solve these challenges:

1. The Virtual DOM
1. A component-based architecture
1. The introduction of JSX

### The Virtual DOM

The flowchart below depicts the steps the browser must perform to render a change to the page:

![dom_render](https://media.git.generalassemb.ly/user/17300/files/9bbd3300-311a-11ea-9ba5-2ec0144463c1)

It's a complicated process that affects the performance of our applications, especially on devices with slower processors, such as mobile devices. Now, consider how we've been displaying information from external APIs. Conventionally, we make a request to an API, get back data and then use JavaScript to update the page contents. When new requests are made, some of the data may have changed, but much of it probably did not. Nevertheless, each time a new request is made, we update all of the page contents from the API data.

It would be far better if we could determine exactly what has changed in the data and then only render the changes. Doing so could eliminate some or all of the render processes needed to update the page. This is exactly what the Virtual DOM in React does for us!

![virtual_dom](https://media.git.generalassemb.ly/user/17300/files/4124d680-311c-11ea-8675-8eeed9667c10)

In the diagram above, our data is represented on the left. In software architecture terms, we often refer to this as the **Model**. In the middle, is the React's Virtual DOM. It uses the data to build a version of the DOM in memory. It then compares it to the previous copy it has in memory. If there are any differences between the two, it patches the changes into the DOM to update the page, which we refer to as the **View** in our application's architecture.

### Components

Components are a way to split the UI of your application into **independent**, **reuseable** pieces. As developers, this helps us reduce duplication in our code and it makes it easier for us to reason about each piece of our UI in **isolation** from the larger, more complex, overall application.

Components can be as small as an individual button or as large as an entire page. You can think of them as LEGO®s for your application's interface. Individual LEGO pieces come in lots of different sizes and shapes, and you can combine them to build pretty much anything. In React, we combine components to build up our application. Well-built React components can even be reused in different applications just as the parts from different LEGO sets can be used interchangeably.

### JSX

Strictly speaking, JSX isn't exclusively a React syntax, but it was built by the folks at Facebook and introduced with an early version of React. **JSX is a syntax extension to JavaScript** that allows us to write code that looks a lot like HTML inside of our JavaScript files. This makes it much faster to build components and easier for us to reason about the interfaces we create in React.

## Exercise: Thinking in React (6 mins)

In your groups, briefly review how the React docs recommend breaking up a mockup into components in the first couple of paragraphs of this post on [_Thinking in React_](https://reactjs.org/docs/thinking-in-react.html) up to **Step 2**.

With that in mind, take a look at this page on [Craigslist](https://boston.craigslist.org/d/apts-housing-for-rent/search/apa) and answer the following questions:

- How would you apply what you've learned so far about React to break the UI into components?
- What might be an example of a nested component?
- Which components are reused on the page?

## The Movie App

Throughout this lesson, we'll be building a simple application in React together. This application will display some static movie data. To get started, we're going to use a popular tool called [**Create React App**](https://create-react-app.dev/) to scaffold our React application.

### I do: Creating a React Application

Watch as I create a React application using Create React App. First, I'll move into the `sandbox` directory where I want to create my project directory. Then, I'll run the Create React App from the command line, which will create the project directory for me and all of the files I need to make my application run.

### You do: Create and Start a React Application

On your own, create a React application:

1. In the Terminal, type: `cd ~/sei/sandbox` and press enter.
1. Once you're in the **sandbox** directory, type `npx create-react-app movie-app` and press enter.
1. After it's completed and you're returned to the prompt, type `cd movie-app`.
1. Next, open the application in VS Code by typing `code .`.
1. Back in the Terminal, type `npm start` to launch the development server.

## Project Structure

Let's explore some of the files that have been created in the project:

```
├── node_modules
├── public
|   ├── favicon.ico
|   └── index.html
├── package.json
├── yarn.lock             (delete this)
└── src
    ├── App.css
    ├── App.js
    ├── App.test.js       (safe to delete)
    ├── index.css
    ├── index.js
    ├── logo.svg
    ├── serviceWorker.js
    └── setupTest.js      (safe to delete)
```

1. **index.html**: The page that will be loaded by the browser. Since browsers only understand HTML, CSS, and JS, so everything we write will be converted into JS and automatically injected into this file so that it can be loaded by the browser. **We don't modify this file except for the page `title`.**
1. **src/index.js**: This is the main entry point for our JavaScript and its job is to render the top-level App component into the browser's DOM. **We won't modify this file**.
1. **src/App.js**: As our top-level component of our React application, the App component will load all of our other components as **_descendants_**.

## Creating Components in React

Lets take a closer look at the `App.js` file that makes up our App component. Aside from the unfamiliar `import` statements at the top of the page and the `export` at the bottom of the page, all we have here is a JavaScript function that returns a bit of **JSX**!

```jsx
function App() {
  return (
    <div className="App">
      <header className="App-header">
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}
```

> In this case the `return` statement is enclosed in some parentheses so that it can break over several lines to make it more readable, but don't let that throw you off. This is just a plain old JavaScript function.

Inspect the page in the browser using the developer tools and compare the HTML that was generated by React with the JSX in the function above.

- What's the same?
- What's different?
- This is where the App component is defined. How do you think it's getting on the page?

### We Do: Modify the App Component

Let's test out our theory about JSX works. Select everything inside of the App function and replace it with `return <h1>Hello World</h1>;`. Now check it out in the browser.

### I Do: Create a Function Component

Observe how I create a new file in the `src` directory to create a new component. Keep an eye on how I name the file and the component. Also be on the look out for how the component is added to my `App.js` file.

## Function Components in React

Function components in React use Javascript's function syntax to define the HTML that the component will produce and the behaviors it will have. In order to make our application modular and components more easily reusable, we separate each component into individual files and use an `export` statement to expose the function so that it can be imported into other files.

### Basic Structure

```jsx
import React from 'react';

// Function name has an initial cap
function Header() {
  // The return statement must return a single element
  // Parentheses group the JSX so that
  // it can break over several lines for readability
  return (
    <header>
      <h1>Hello World!</h1>
      <h2>⭐️ Welcome to React ⭐️</h2>
    </header>
  );
}

// Export the Header so that it can be imported in other files
export default Header;
```

## Composing Components

Components can be rendered to the page using different methods in React, but the most common way this is done is through **_component composition_** — referring to a component in a parent's output.

```jsx
import React from 'react';
// Import the component from the same directory
import HelloWorld from './HelloWorld';

function App() {
  // Compose the component inside of the App's return
  return <HelloWorld />;
}

export default App;
```

## Components Summarized

There are a few things we have to remember when creating components in React.

- All component files **must** import React.
- Function components must return **a single element**. Sibling elements must be contained in a single outer wrapping element.
- They always receive one argument (a **props object**).
- Components are named with an **initial cap**.
- You can surround any return value in parenthesis to break it on to multiple lines.
- To import a custom component, use the relative path to the file. All component imports must start with `./` to reference the current directory, or `../` to reference a parent directory.

## You Do: Create a Header Component

Create a header component that produces the following HTML when rendered on the page:

```html
<header>
  <h1>Reelz: The Movie App</h1>
  <div>
    <ul>
      <li>Now Playing</li>
      <li>Must See Movies</li>
    </ul>
  </div>
</header>
```

Make sure to import your component into the `App.js` file and compose it in the App components output to make it display on the page.

## Component Props

In order to make our components truly reusable, we need a way to pass them the unique data that they are meant to display. In React we do this with **_props_**. Let's see how:

### We Do: Create a Welcome Component

We want to welcome users to our site. So let's create a simple Welcome component together that outputs the message inside the Header component that we created. The HTML we'll want to render is:

```html
<p>Welcome, User!</p>
```

<details>
  <summary>Solution</summary>

```jsx
import React from 'react';

function Welcome {
  return <p>Welcome, User!</p>;
}

export default Welcome
```
</details>

Obviously this is a little impersonal, so let's use props to put a name on the page. _Every component is passed a props object as an argument in React._ We can see this if we add a parameter to our component and log out its value inside the component function. Right now, it's an empty object but we can pass any data we want to our components through it. Let's give that a try.

Inside the Header component where the Welcome component is rendered, change the Welcome component to add the following:

```jsx
<Welcome name={'YourName'} />
```

What you should see in the console now is the object with a key value pair representing the name and the string value you set.  We can add any kind of values we want here, we're not just limited to strings.  Let's try adding a boolean:

```jsx
<Welcome name={'YourName'} newUser={true} />
```

> #### :triangular_flag_on_post: IMPORTANT:
> Remember JSX is _an extension_ to the JavaScript syntax, so we **cannot** use any [reserved words](https://www.w3schools.com/js/js_reserved.asp) as a prop name.  This is the reason we use `className` instead of `class` to add CSS classes to elements in JSX.

### JavaScript Expressions in JSX

We've seen that the JSX inside a component's `return` statement is what the component renders as HTML.  JavaScript expressions are also valid inside of the return statement of a React component.  To use a JavaScript expression, we need to surround it in `{}` braces.

To access the props inside of our return, we'll write:

```jsx
function Welcome (props) {
  return <p>Welcome, {props.name}!</p>;
}
```

All of the following are JavaScript expressions, and therefore valid inside of the JSX in a component's `return` statement:

- Variables `{name}`
- Arithmetic `{2 + 2}`
- Ternary operators `{hour > 11 ? 'PM' : 'AM'}`
- Logical operators `{holiday && 'Happy Holiday!'}`
- Left-side expressions `{arr.map(el => <li>el.name</li>}`

## You Do: Display a Custom Message

Display a custom message to the user based on whether the `newUser` prop is set to `true` or `false`.   If the value is `true`, the message should read: "Welcome aboard!" followed by the user's name.  If the value is `false`, the message should read: "Welcome back!" followed by the user's name.

<details>
  <summary>Solution</summary>

```jsx
import React from 'react';

function Welcome (props) {
  const message = props.newUser ? 'Welcome aboard' : 'Welcome back'
  return <p>{message}, {props.name}!</p>;
}

export default Welcome
```
</details>

### Explore on Your Own

Test adding props of different datatypes.

- What happens if you try to render an array?
- What happens if you try to render a whole object?
- Can you pass a function as props?

## Props Summarized

- Props are the key value pairs that are passed to the props object
- Props can be passed any datatype using curly braces`propName={any datatype here}`
- Props cannot be named using a JavaScript reserved keyword.
- There is no limit to the number of props that can be passed to a component (except readability and common sense 😵)

## You Do: Create a Movie Component

Our movie app needs to display some movies. First, add the following variable above the App component function:

```js
const movie = {
  title: 'Star Wars: The Rise of Skywalker',
  poster: 'https://image.tmdb.org/t/p/w500/db32LaOibwEliAmSL2jjDF6oDdj.jpg',
  rotten_tomatoes: 53,
  audience_score: 86,
  summary:
    'The surviving Resistance faces the First Order once again as the journey of Rey, Finn and Poe Dameron continues. With the power and knowledge of generations behind them, the final battle begins.'
}
```

Your rendered component output should look like this:

```html
<div class="movie">
  <h2>Star Wars: The Rise of Skywalker</h2>
  <img src="https://image.tmdb.org/t/p/w500/db32LaOibwEliAmSL2jjDF6oDdj.jpg" alt="movie poster" />
</div>
```

### We Do: Create an Movies Component

An app that displays only one movie isn't much of a movie app so we'll create a component that will display a bunch of movies.  First, we need more data.

1. Create a new file called `data.js` inside the `src` directory.
1. Copy the contents of the [data file](data.js) in this repository.
1. Paste the contents inside of the newly created file in your movie app.
1. Import the file into the App component using the following syntax:

```js
import { movies } from './data'
```

This special syntax is called **_destructuring_** and we'll be using a lot in React, but more on that later.  To test that our data is loaded, add `console.log(movies)` above the App function and check you see the movies array in the console.

Now we need to do some clean up.  Delete the movie object, the Movie component and its import statement from App.  We'll be composing the Movie component in the Movies component instead.

### On Your Own

Create a new component called **Movies** that renders the following HTML when imported and rendered in the App:

```html
<section>
  <h2>Now Playing</h2>
</section>
```
> Remember that you can only return a single element in a component.  So you'll need to wrap your Header and Movies inside a single element.

#### Pass the Movies Component Data

We have access to our data inside the App component stored in a variable called `movies`.  How do we get it to our Movies component?

<details>
  <summary>Solution</summary>

With `props` of course!

```jsx
function App () {
  return (
    <>
      <Header />
      <Movies movies={movies} />
    </>
  );
}
```
</details>

### Accessing the Data in Movies

Inside of our Movies component, we need to add our Movie components.  Let's make one Movie to start:

```jsx
function Movies (props) {
  return (
    <section>
      <h2>Now Playing</h2>
      <Movie title={movies[0].title} image={movie[0].poster} />
    </section>
  )
}
```

### Display All of the Movies

While this approach works for us, its not very practical.  We need a way to display an unknown number of movies. Earlier we saw that if you try and render an array, React is smart enoungh to just drop the brackets and display all of the data. We also saw that if we try to render an object the whole app breaks.

To solve this, we need to create a new array from the existing one that contains a bunch of JSX elements.  Array iteration methods can help us to do that easily! In this case we want the new array to have the same length as the movies array so the `.map()` method is the one we'll use:

```jsx
function Movies (props) {
  return (
    <section>
      <h2>Now Playing</h2>
      {movies.map(movie => (
          <Movie key={movie.id} title={movie.title} image={movie.image} />
        ))}
    </section>
  )
}
```
## Additional Resources

- [React Components | Codecademy](https://www.codecademy.com/courses/react-101/lessons/your-first-react-component)
- [Intro to Components | GA Video](https://generalassembly.wistia.com/medias/h64z7lp1ir)
- [React Components and Props | React Docs](https://reactjs.org/docs/components-and-props.html)
- [React Component Props | Codecademy](https://www.codecademy.com/courses/react-101/lessons/this-props)

## [License](LICENSE)

All content is licensed under a CC­BY­NC­SA 4.0 license.

All software code is licensed under GNU GPLv3. For commercial use or alternative licensing, please contact legal@ga.co.
