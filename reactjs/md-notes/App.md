# Basic class App

```javascript
import React, { Component } from "react";

class App extends Component {
  constructor(props) {
    super(props);
    ...
  }

  state = {
    key1: value1,
    key2: value2,
  };

  pressButtonHandler = (event) => {
    ...
  };

  render() {
    return;
    <div>
      <input onChange={this.pressButtonHandler}/>
    </div>;
  }
}
```
