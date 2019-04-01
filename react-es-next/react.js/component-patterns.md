# Component Patterns

## export default Class

```javascript
import React, { Component } from 'react';

class Button extends Component {
  render() {
    // ...
  }
}

export default Button;
```

### inline

```javascript
import React, { Component } from 'react';

export default class Button extends Component {
  render() {
    // ...
  }
};
```

## export default function

```javascript
import React from "react"; // should import React, not react

const hello = props => 
  <div>
    <h1>Hello CodeSandbox</h1>
  </div>

export default hello
```

### inline

```javascript
import React from "react"; // should import React, not react

export default props => 
  <div>
    <h1>Hello CodeSandbox</h1>
  </div>
```

## Pure Component



### Pure Component vs. Stateless component







