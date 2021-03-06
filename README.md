# usePromiseSubscription

Custom React Hook that properly awaits a promise to resolve.  
It automatically 'unsubscribes' if the component is unmounted.

Here's an example on CodeSandbox:  
[![Edit pkk3xjn00m](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/pkk3xjn00m?fontsize=14)

## Requirements:

* React 16.8.0 or higher

## Install

For now you can install from GitHub:
```
npm install https://github.com/JulianG/use-promise-subscription.git
```
or
```
yarn add https://github.com/JulianG/use-promise-subscription.git
```

## Use

Import the function:

```js
import { usePromiseSubscription } from 'use-promise-subscription';
```

### Basic usage:
```js
const App = ({ client }) => {

  const [bananas] = usePromiseSubscription(client.fetchBananas, [])

  return (
    <ul>
    {bananas.map(banana => <li>{banana}<li>)}
    </ul>
  )
}
```
The first render will use the empty array passed as a default value.  
The next render will -probably- have some bananas in the `bananas` array.

**Note that there is no need to `useState` to keep track of `bananas`.**

### Advanced usage:

Handling errors and loading state.
```js
const App = ({ client }) => {

  const [bananas, error, pending] = usePromiseSubscription(client.fetchBananas, [])

  return (
    <ul>
    {pending && <li>Loading...</li>}
    {!pending && error && <li>Error! {error.toString()}</li>)}
    {!pending && !error && bananas.map(banana => <li>{banana}<li>)}
    </ul>
  )
}
```
On the first render `pending` is true and the "loading" message is rendered.  
The next time the promise will have resolved or rejected.
`error` will be 'truthy' if the promise was rejected, and error message can be displayed.
In most cases the promise will have resolved and the `bananas` array is displayed.

----


## Develop

* yarn install
* yarn test
* yarn build

```









```

----

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.<br>
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br>
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.<br>
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.<br>
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br>
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (Webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).
