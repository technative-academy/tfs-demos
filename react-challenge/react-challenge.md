# React challenge

We’re going to set up a new React app. Then we'll be ready to add some examples of the React logic and functionality that we've been learning.


## Creating a new React App

The first thing we need to do is find somewhere on our computer to create our new project.

In a terminal window, navigate to the location we want to create the new app:

```bash
cd path/to/a/folder
```

Next, we can either use [Vite](https://vite.dev/) or [Create React App](https://create-react-app.dev/) to generate our new project.

We can call the project whatever we like, for this tutorial we will call it `react-challenge`.

If you want to use Vite (recommended), use the following command:

```bash
npm create vite@latest react-challenge -- --template react
```

If you want to use Create React App, use the following command:

```bash
npx create-react-app react-challenge
```

In the terminal we may be asked some questions, it's usually fine to accept the default options.

Next we'll navigate into the new folder:

```bash
cd react-challenge
```

Depending on which of the two commands you used above, you may have to install dependencies with `npm install`

We'll get the files open in VS Code:

```bash
code .
```

We might find that it's helpful here to have two terminal tabs open, one that runs the app and a second that we can use for git (more on this shortly).

In one terminal tab, start the app running `npm run dev` if you used Vite or `npm start` if you used Create React App


Finally, we'll open it in a web browser (if this didn't happen automatically) - if you used Vite it's [http://localhost:5173/](http://localhost:5173/) and if you used Create React App it's [http://localhost:3000/](http://localhost:3000/)

Don't forget to open the browser's dev tools and switch to the console tab, this will be useful in case we have any errors.


---

## Initial set-up

There are some default files and folders for us. We can start to modify them to customise our new project. They're slightly different depending on which of the two services you used

### Root folder

- `package.json` - we don't tend to update this often, and usually these updates are made automatically, but this is where we record a list of all the dependencies that we import for our project
- `README.md` - here are some default notes on Create React App, we can leave them for now but we might want to customise some of this later to describe our project.
- `index.html` - we may want to update this in a few places, for example to change the `<title>` value that appears in the browser tab bar

### `src` folder

- `main.jsx` or `index.js` - this is the first/home file of our React app - all logic for our application starts here. We can see that it currently imports two files: `index.css` and `App.jsx` - we'll change this shortly
- `index.css` - these are some default styles for the website - we'll move this shortly

#### App component

This is our first default component that the service has generated for us. There are some relevant files:

- `App.jsx` - the component itself
- `App.css` - styles for the component

Actually we're going to stop using this component fairly quickly because we don't want it in our app. We'll see that shortly too.


#### Optional: Prettier

It's usually worth setting up prettier for projects like this, so we can ensure that our code is auto-formatted on save.

We may all have prettier configured differently, for example we might prefer tabs over spaces, or two spaces to a tab rather than four - whatever our personal preferences. We create a prettier config file in the repo to contain these preferences. This file should be saved in the root of the repo.

There are several name options that we can call this file, such as `.prettierrc.json` - note the `.` at the start of the file name is important!

It's contents can just be an empty object for now:

```js
{}
```

That may be enough to get prettier running on save. If it doesn't, we may also need to create a `.vscode/settings.json` config file to tell Visual Studio Code to run Prettier every time we save a file:

```
{
    "editor.defaultFormatter": "esbenp.prettier-vscode"
    "[javascript]": {
        "editor.formatOnSave": true,
    },
    "[javascriptreact]": {
        "editor.formatOnSave": true,
    },
    "[css]": {
        "editor.formatOnSave": true,
    }
}
```

Test this by changing the default formatting of a JS file, and a CSS file, and check that they are both reformatted on save as expected.


#### Out of scope

There may be a few other files that are in the project but out of scope for this tutorial - we can look into them another time.

---

## Git (and GitHub)

The first thing we're going to do is set up git (and GitHub) so that we can track the changes we're making to the project.

In a terminal window we check the status of the current project:

```bash
git status
```

if it is already a git directory, there will already be a initial commit.

If not, we can run `git init` to initialise git for this project.

Next, we should create a new repository in Github so that we can push our repo there.

Once the repository is set up in GitHub, follow their instructions to add a new 'origin' to our local repository, and then push it up to GitHub.


### Optional: Add deployments to Netlify

This is an optional step but it would be good to also set up Netlify to allow us to deploy the app to Netlify so we can see it online. This will allow us to share it once it's complete.

Once set up, copy the link to the deployed app on Netlify and add it to the repo in GitHub, so that it appears in the right-hand sidebar of the project repository.

---

## Folder structure

Next we're going to set up a basic folder structure. This will help to keep the project manageable when we start to add a lot of files.

There is no right or wrong way to do this, if we look for articles about React folder structures we'll find _a lot_ of opinions.

For now we're going to create a folder called `components`. Then, for each component we'll create a dedicated sub-folder:

```bash
mkdir src/components
```

(We could create this folder inside VS Code if that's easier than via the terminal)


### assets

We're also going to create a folder called `assets` - this is where we'll store any static files, e.g. images, CSS files and fonts.

```bash
mkdir src/assets
mkdir src/assets/images
mkdir src/assets/css
```

### CSS

To tidy up the `src` folder we can move our `index.css` file into the new `src/assets/css` folder.

If we do this, we need to remember to update the reference to it in the `index.jsx` file:

```css
import './assets/css/index.css';
```

While we're looking at the `index.css` file, we may want to edit it to put in some site defaults, for example we could set a few default styles:

```css
html {
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}

html,
body {
  height: 100%;
}

body {
  margin: 0;
  padding: 0;
  font-family: Helvetica, sans-serif;
}

#root {
  height: 100%;
}
```

### CSS modules

The CSS above is useful 'global' CSS that will apply across the app.

For all other CSS, especially the CSS that is created for each component, we're going to use [CSS Modules](https://create-react-app.dev/docs/adding-a-css-modules-stylesheet).

This is set up already with Create React App, so we can use it immediately.

The advantage of this approach is that it ensures there won't be any conflicts between styles, so we can use simple class names (rather than needing a naming convention such as BEM).

---

## Components

We're going to create some new components to give our site some structure. Soon it will look something like this:

<style>
.page-layout-example-1 header,
.page-layout-example-1 nav,
.page-layout-example-1 main,
.page-layout-example-1 footer {
    padding: 2%;
    border: 1px solid lightgray;
    display: flex;
    align-items: center;
    justify-content: center;
}
.page-layout-example-1 header,
.page-layout-example-1 footer {
    color: white;
    background: grey;
}
.page-layout-example-1 header {
    padding: 5%;
}
.page-layout-example-1 nav {
    background: lightgrey;
    padding: 2%;
}
.page-layout-example-1 main {
    height: 200px;
    flex: 1
}
</style>

> <div class="page-layout-example-1">
>   <header>SiteHeader</header>
>   <nav>SiteNav</nav>
>   <main>
>     MainContent
>   </main>
>   <footer>SiteFooter</footer>
> </div>


### App component

We're not going to delete the App component from the repo because it might be a useful reference to look back at in future, but we're not going to display it in our app.

Create a folder inside `components`, call it `App`, and move the four App-related files in there:

- `App.jsx`
- `App.css`
- `logo.svg`
- `App.test.js`

We also need to remove the reference to the `App.jsx` file in our main `index.jsx` file, we no longer need it there as we're going to add our own content instead. We can replace it with an empty `<div/>` element for now - we'll replace it with the real content shortly.

If we look at our website in a browser now we should just see an empty page. That's fine, we'll add some content shortly!


### Root component

We're going to start with a `Root` component, this will be the first component in our new app.

We don't _need_ to have a `Root` component, it just keeps our core page structure tidy, and separated from our `index.jsx` file.

```
mkdir components/Root
touch components/Root/Root.jsx
```

Let's create a basic file for now, we'll add to it shortly:

```jsx
function Root() {
  return (
    <div className="wrapper">
      Root
    </div>
  );
}

export default Root;
```

We will replace the default text shortly, it's just in there for now to check that it renders as expected in our app.

Update the main `src/index.jsx` file - import this new `Root` component (rather than the old `App` component that was there previously):

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import Root from './components/Root/Root';
import './assets/css/index.css';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <Root />
  </React.StrictMode>
);
```

Look in the browser and see if it just shows the word 'Root'.

So far so good!


#### Root css

In the same folder as the `Root` component, create a file called `Root.module.css`

Add the following styles:

```css
.wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100%;
}
```

To import this CSS file to our component - and to take advantage of [CSS modules](https://create-react-app.dev/docs/adding-a-css-modules-stylesheet) - we need to make two updates to our `Root` component.

First, we need to import these styles, this could be added as the first line of the component:

```jsx
import styles from "./Root.module.css";
```

Then, in the component itself, we want to reference a class from the CSS.

Change this line:

```jsx
<div className="wrapper">
```

To this:

```jsx
<div className={styles.wrapper}>
```

Our `Root` component should now look like this:

```jsx
import styles from "./Root.module.css";

function Root() {
  return (
    <div className={styles.wrapper}>
        Root
    </div>
  );
}

export default Root;
```


### SiteHeader component

Create a new folder in `components` and call it `SiteHeader`

Within this, create a file called `SiteHeader.jsx`

```jsx
import styles from './SiteHeader.module.css';

function SiteHeader() {
  return (
    <div className={styles.wrapper}>
      SiteHeader
    </div>
  );
}

export default SiteHeader;
```

#### SiteHeader css

In the same folder, create a file called `SiteHeader.module.css`

Add the following styles:

```css
.wrapper {
  padding: 2rem;
  border: 1px solid lightgray;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  background: grey;
}
```

### SiteNav component

Create a new folder in `components` and call it `SiteNav`

Within this, create a file called `SiteNav.jsx`

```jsx
import styles from './SiteNav.module.css';

function SiteNav() {
  return (
    <div className={styles.wrapper}>
      SiteNav
    </div>
  );
}

export default SiteNav;
```

#### SiteNav css

In the same folder, create a file called `SiteNav.module.css`

Add the following styles:

```css
.wrapper {
  padding: 1rem;
  border: 1px solid lightgray;
  display: flex;
  align-items: center;
  justify-content: center;
  background: lightgrey;
}

.links {
  display: flex;
}

.activeLink,
.inactiveLink {
  padding: 0 2rem;
}

.activeLink {
  color: #000;
}

.inactiveLink {
    color: #666;
}
```

### MainContent component

Create a new folder in `components` and call it `MainContent`

Within this, create a file called `MainContent.jsx`

```jsx
import styles from './MainContent.module.css';

function MainContent() {
  return (
    <div className={styles.wrapper}>
      MainContent
    </div>
  );
}

export default MainContent;
```

#### MainContent css

In the same folder, create a file called `MainContent.module.css`

Add the following styles:

```css
.wrapper {
  border: 1px solid lightgray;
  display: flex;
  align-items: stretch;
  justify-content: center;
  width: 100%;
  flex: 1;
}
```

### SiteFooter component

Create a new folder in `components` and call it `SiteFooter`

Within this, create a file called `SiteFooter.jsx`

```jsx
import styles from './SiteFooter.module.css';

function SiteFooter() {
  return (
    <div className={styles.wrapper}>
      SiteFooter
    </div>
  );
}

export default SiteFooter;
```

#### SiteFooter css

In the same folder, create a file called `SiteFooter.module.css`

Add the following styles:

```css
.wrapper {
  padding: 1rem;
  border: 1px solid lightgray;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  background: grey;
}
```

### Updating Root

Now that we have some components to add to our site, we can import them in the `Root` component:

```jsx
import styles from "./Root.module.css";

import SiteHeader from "../SiteHeader/SiteHeader";
import SiteNav from "../SiteNav/SiteNav";
import SiteFooter from "../SiteFooter/SiteFooter";
import MainContent from "../MainContent/MainContent";

function Root() {
  return (
    <div className={styles.wrapper}>
      <SiteHeader />
      <SiteNav />
      <MainContent />
      <SiteFooter />
    </div>
  );
}

export default Root;
```

Test this in a browser, see if it looks like the example layout at the start of the 'components' section above.

We can customise these styles later, this is just an initial layout to get you started.


---

## React Router

Now that we have our core layout set up, we can start to add our pages (also sometimes called views, because we no longer have distinct pages as we do with HTML. We can refer to these in different ways but here we'll stick to views).

We will want a view for each of our experiments.

To navigate between them we're first going to set up React Router.


### Installation

We can add React Router with the following command:

```bash
npm install --save react-router-dom
```

The [React Router tutorial](https://reactrouter.com/6.30.1/start/tutorial) is a good reference for how this works.


### Adding the router to our app

#### Creating routes

We're going to create two new views - a 'home' view and an 'about' view.

Once we have this working we'll create several more views, but for now this is enough of a proof of concept to ensure that the routing works.

For each of these two new views, we need to create a sub-folder in the `components` folder, and then add a JavaScript file containing the following.

The example below would be for an "About" page, where the file would be `src/components/About/About.jsx`:

```jsx
import styles from './About.module.css';

function About() {
  return (
    <div className={styles.wrapper}>
      <p>About</p>
    </div>
  );
}

export default About;
```

And corresponding file CSS:

```css
.wrapper {
  background: #f90;
  width: 100%;
}
```
(You would follow the same pattern for a Home component, replacing `About` with `Home`)


#### routes.jsx

We want to set up a file where we can reference all our routes and their corresponding components.

We'll create a new file called `routes.jsx` in the `src` folder.

This is where we list all of the new views we just created, in the `children` array of the `Root` view:

```jsx
import Root from "./components/Root/Root";
import Home from "./components/Home/Home";
import About from "./components/About/About";

const routes = [
  {
    path: "/",
    element: <Root />,
    children: [
      {
        path: "",
        element: <Home />,
      },
      {
        path: "about",
        element: <About />,
      },
    ],
  },
];

export default routes;
```


#### index.jsx

Now we have a file for our routes, we can add the router to our `index.jsx` file - note that we have replaced the `Root` component that we had here before:

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import routes from "./routes";
import "./assets/css/index.css";

const router = createBrowserRouter(routes);

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);
```


### Updating existing components

#### MainContent

In the `MainContent.jsx` component we need to add an `Outlet` - this is where the routes will be displayed:

```jsx
import { Outlet } from "react-router-dom";

import styles from './MainContent.module.css';

function MainContent() {
  return (
    <div className={styles.wrapper}>
      <Outlet />
    </div>
  );
}

export default MainContent;
```

#### SiteNav

We need to create links to each of our new views in the `SiteNav` component:

```jsx
import { NavLink } from "react-router-dom";
import styles from "./SiteNav.module.css";

function SiteNav() {
  const navLinks = [
    { label: "Home", url: "/" },
    { label: "About", url: "/about" },
  ];
  return (
    <div className={styles.wrapper}>
      <nav className={styles.links}>
        {navLinks.map((navLink) => (
          <NavLink
            key={navLink.url}
            to={navLink.url}
            className={({ isActive }) =>
              isActive ? styles.activeLink : styles.inactiveLink
            }
          >
            {navLink.label}
          </NavLink>
        ))}
      </nav>
    </div>
  );
}

export default SiteNav;
```

### Test the app!

We should now have a working React app with a header, nav and footer, and two views in the main content area that we can switch between. The URL should be updated when we move between the views.


---

## Ideas for further updates

### Customise the app

- Update the page title (and any other values) in the `public/index.html` page
- Update the favicon
- Update the SiteHeader with more relevant content
- Update the SiteFooter with more relevant content
- Update the default page styles, e.g. the font and colours
- Write some initial content for the home and about pages
- Update the README.md file
- Add some tests (see the App component test file for an example)


### Creating more views

Now that we have a basic site structure set up, we can create some more views.

We could create a view for each piece of functionality that we've been learning, for example:

- forms
- `useState` hook
- `useEffect` hook
- (etc)

Each of these views will help us to demonstrate and test what we've been learning.

For each of the views we can add custom content and styles.


### Sub-views

We could create a new view, for example 'hooks', and then within this view we could create a second level of navigation, e.g. for different types of hook.
