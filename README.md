# Importing and Exporting in React

## Problem Statement

## Objectives


## A Quick Note on Exporting

As with good programming practices, we want to write modular code. That is, we
want to split our code up into logical sections/separate files. One common
practice in React is for each individual component to be stored in a separate
JavaScript file.

```dir
|-- src',
   |-- components',
       |-- App.js',
       |-- Form.js',
       |-- Main.js',
       |-- Nav.js',
       |-- Photo.js'
```

All components have an `export` statement, and any component that contains a
_child_ component in its JSX must `import` that component in.

There are a few ways
Go ahead and create a `/src` directory in this repository and add `index.js` to it.

Let's practice writing modular code by creating a new file in
`/src/components/foo.js` (you'll also need to create the `/src/components/`
directory). In that file, we'll add this content:

```js
export const message = "I am a component!";
```

We can import this component in our `index.js` by using `import` and referencing the origin file:

```js
import { message } from './components/foo';
```

Note that files are always referred to using a relative path (even if they are
in the same directory). This way Node knows whether to look for a local module,
one found in `node_modules`, or in the global modules.

Back to the exporting stuff! Using CommonJS, we have two options of exporting
things out of our files: either through named exports (exporting multiple
things) or a default export (exporting one thing).

### Named exports

Named exports allow us to export several things at once. This is useful for
utility modules or libraries. Exporting several things at once is done by
exporting an object. Because we are exporting this object as default without a
name, we can assign it any name when we import it (in this case "fruit").

```js
// In a file called `fruits.js`
export default {
  apple: 'red',
  banana: 'yellow',
};

// In a file in the same directory
import fruit from './fruits';
console.log(fruit.apple); // prints 'red'

// In another file, also in the same directory
import { apple } from './fruits';
console.log(apple); // prints 'red'
```

When using named exports, we can choose to either import the entire thing and
then reference the keys on the exported object, or we can import one specific
key.

### Default export

A default export means we're exporting just one thing. This is useful for
exporting components in their own file, since there's only one thing there: the
component itself. Exporting one thing only is done by exporting a reference to
what we want to export. You can also inline the value of what you want to
export.

```js
// In a file called `Tweet.js`
import React from 'react';

class Tweet extends React.Component {
  render() {
    return (
      <div className="tweet">
        <img src="http://twitter.com/some-avatar.png" className="tweet__avatar" />
        <div className="tweet__body">
          <p>We are writing this tweet in JSX. Holy moly!</p>  
        </div>
      </div>
    );
  }
}

export default Tweet;

// In a file in the same directory
import Tweet from './Tweet';
import ReactDOM from 'react-dom';

ReactDOM.render(
  <Tweet />,
  document.getElementById('root')
);
```

You'll mostly be using this method. It's important to correctly export your
components, otherwise the tests can't access the code you've written, causing
them to fail!


#### Resources (if applicable)

### Conclusion
