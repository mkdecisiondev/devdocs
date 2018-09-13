# React

React is a JS UI library that helps build component-based, stateful, performant applications. React itself does not
provide UI components. Our component library of choice is [Material UI](https://material-ui.com/), a React
implementation of Google's Material Design. React is used in [Gatsby](https://www.gatsbyjs.org).

## Learn React

* [Official docs](https://reactjs.org/docs/hello-world.html) (read at least Main Concepts and Advanced Guides)
* [Redux](https://redux.js.org/basics) (read Basics and Advanced)

## Component design

1. Start with a completely stateless UI - build the UI elements in JSX, accepting props as needed
1. If the component meets the needs then you are done!
1. If you need to fetch or calculate data, manipulate props, or manage state, rename your module to `MyModuleTemplate`
1. Now create a new `MyModule` and add all necessary logic, passing props and handlers to `MyModuleTemplate`
