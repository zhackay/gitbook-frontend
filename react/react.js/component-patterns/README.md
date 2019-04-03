# Component Patterns

## export default Class

{% tabs %}
{% tab title="First Tab" %}
```javascript
import React from 'react';

class Button extends React.Component {
  render() {
    // ...
  }
}

export default Button;
```
{% endtab %}

{% tab title="Second Tab" %}
```javascript
import React, { Component } from 'react';

class Button extends Component {
  render() {
    // ...
  }
}

export default Button;
```
{% endtab %}
{% endtabs %}

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



