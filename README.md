# Practice: Action Creator and Reducer Setup

In this short practice, you will load an array of articles into Redux state. You
will then create an [action creator][action-creator] and a [reducer]. When the
_action creator_ sends an action to the _reducer_, the reducer will update the
global state (or not) based on the _action type_. You will connect the reducer
to the store and test your action creator using the `window` object in the
browser DevTools.

## Setup

Click the `Download Project` button at the bottom of this page to go to the
starter repo, then load the repo into [CodeSandbox].

## Action Creator

Start by creating an __articleReducer.js__ file in the __src/store__ directory.

Since there is no database, import the data that is stored in
__src/data/data.json__, assigning it to the variable name `articles`. This data
will be used as the _payload_ for the action creator you are about to create.

Define and export an action creator function called `loadArticles`. It should
have a `type` key with a constant variable value of `LOAD_ARTICLES`. (Before
your action creator, declare your `LOAD_ARTICLES` constant variable and assign
it the string `'article/loadArticles'`.) The `loadArticles` action creator should
also have a payload of the articles that were imported. You can put the payload
under the key `articles`.

If you have done this correctly your code will look similar to this:

```js
import articles from `../data/data.json`;

const LOAD_ARTICLES = 'article/loadArticles';

export const loadArticles = () => {
  return {
    type: LOAD_ARTICLES,
    articles
  };
};
```

## Reducer

Write an `initialState` variable that is assigned to an object. The object
should hold an array with the key of `entries` and the value of an empty array.
The object should also hold another key, `isLoading`, with a boolean value of
`true`.

Create an `articleReducer` function. Every reducer function takes two arguments,
`state` and `action`. Inside the `reducer` function, create a `switch`/`case`
statement that switches based on an action's type. The first action type it
should check for is `LOAD_ARTICLES`. If `action.type` is `loadArticles`, it
should return a new **copy** of the `state` object and update the `entries`
array with the `articles` payload from the `loadArticles` action creator. Be
sure not to mutate the original state! As the `default` case, simply return the
original `state`. Finally, make `articleReducer` the `default` export for
this file.

If you are successful, your added code should be similar to this:

```js
const initialState = { entries: [], isLoading: true };

const articleReducer = (state = initialState, action) => {
  switch (action.type) {
    case LOAD_ARTICLES:
      return { ...state, entries: [...action.articles] };
    default:
      return state;
  }
};

export default articleReducer;
```

## Connect the reducer to Redux

In the root __index.js__ file of your __store__ directory, import the
articleReducer using the variable name `articleReducer`. Now, add this reducer
to the `combineReducers` function, giving it a key of `articleState` and a value
of `articleReducer`

## Test on the Window

To test if your reducer is working, go to your root __index.js__ and

1. Import the `loadActions` action creator from __./store/articleReducer.js__
    - *Remember: named exports need to be wrapped in { } when being imported.*
2. Add this code beneath your `store` variable:

```js
window.store = store;
window.loadActions = loadActions;
```

In your sandbox browser, click the button to `Open In New Window`. In the
`Console` tab of the DevTools in this new window, type the following code:

```js
store.dispatch(loadArticles());
```

If all is working correctly, you should see the `redux-logger` data in the
console. It will show the `prev state` with an `article.entries` array of `0`,
the `action`, and the `next state` with five articles in the `article.entries`
array.

![redux-logger][redux-logger]

## What you have learned

**Congratulations!** In this practice you have learned how to

1. Create an `action creator`
2. Create a `reducer`
3. Test an `action creator` on the window of the browser using `redux-logger`

[CodeSandbox]: https://codesandbox.io
[action-creator]: https://redux.js.org/usage/reducing-boilerplate
[reducer]: https://redux.js.org/usage/structuring-reducers/basic-reducer-structure
[redux-logger]: https://appacademy-open-assets.s3.us-west-1.amazonaws.com/Modular-Curriculum/content/react-redux/topics/redux/assets/redux-logger-articles.png
[code-sandbox]:http://www.codesandbox.io