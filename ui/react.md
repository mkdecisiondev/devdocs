# React

React is a JS UI library that helps build component-based, stateful, performant applications. React itself does not
provide UI components. Our component library of choice is [Material UI](https://material-ui.com/), a React
implementation of Google's Material Design. React is used in [Gatsby](https://www.gatsbyjs.org).

## Learn React

* [Official docs](https://reactjs.org/docs/hello-world.html) (read at least Main Concepts and Advanced Guides)
* [Redux](https://redux.js.org/basics) (read Basics and Advanced)
* [React TypeScript cheatsheet](https://github.com/sw-yx/react-typescript-cheatsheet)

## Component design

1. Start with a completely stateless UI - build the UI elements in JSX, accepting props as needed
1. If the component meets the needs then you are done!
1. If you need to fetch or calculate data, manipulate props, or manage state, rename your module to `MyModuleTemplate`
1. Now create a new `MyModule` and add all necessary logic, passing props and handlers to `MyModuleTemplate`
1. Determine module state: *do not* store derived values in state, calculate them as needed from other state or props
1. Determine which module state is transitory and which needs to persist
	1. When a component disappears from view, transitory state is lost
	1. State that needs to persist when a component is not visible needs to either be lifted up to a higher component or stored (e.g. in Redux)
