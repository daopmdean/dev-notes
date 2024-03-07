```javascript
React.createElements();
```

## Pass argument to function

```javascript
onClick={
  () => this.callTheFunction(args)
}

onClick={
  this.callTheFunction.bind(this, args)
}
```

## Create a component

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

```javascript
const Welcome = (props) => {
  return <h1>Hello, {props.name}</h1>;
};
```

```javascript
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

## Lifecycle

useEffect do something when the component change

first import

```javascript
import { useEffect } from "react";
```

then use it in the component

```javascript
useEffect(() => {
  ...do something
  return () => {
    ...doing cleanup things
  };
}, [...when something change]);
```

## PureComponent

when to extends PureComponent??

```javascript
shouldComponentUpdate(nextProps, nextState) {
  ...
}
```

when ever any single props of the class change the component will update, otherwise it would not.

## Set state the right way

When you need to update previous State

```javascript
this.setState((preState, props) => {
  return {
    key: preState.doThings,
  };
});
```

## Ref with class base

```javascript
...
constructor(props) {
  super(props);
  this.inputRef = React.createRef();
}

componentDidMount() {
  this.inputRef.current.focus();
}

<SomeComponent ref={this.inputRef} />

...
```

```javascript
...

componentDidMount() {
  this.inputRef.focus();
}

<SomeComponent ref={(inputEle) => {this.inputRef = inputEle}} />
...
```

## Ref with functional component

import first

```javascript
import { useRef } from "react";
```

```javascript
const SomeComp = (props) => {
  const btnRef = useRef(null);
  ...

  useEffect(() => {
    btnRef.current.click();
  });
  ...
  return <SomeThing ref={btnRef} />;
};
```
