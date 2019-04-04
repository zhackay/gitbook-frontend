# React Official Docs

{% embed url="https://reactjs.org/docs/getting-started.html" %}

## 1. Rendering

{% tabs %}
{% tab title="Rendering element into DOM" %}
#### "root" DOM node - everything inside it will be managed by React DOM.

```text
<div id="root"></div>
```

```text
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

###  <a id="updating-the-rendered-element"></a>
{% endtab %}

{% tab title="Updating the Rendered Element" %}
* React elements are [immutable](https://en.wikipedia.org/wiki/Immutable_object). 
  * Once you create an element, you can’t change its children or attributes. 
  * An element is like a single frame in a movie: it represents the UI at a certain point in time.
* When reactDOM.render\(\) is called, React DOM compares the element and its children to the previous one, and only applies the DOM updates necessary to bring the DOM to the desired state.
{% endtab %}

{% tab title="DOM" %}


![](../../../.gitbook/assets/image%20%281%29.png)
{% endtab %}
{% endtabs %}

## 2. Components and Props

### Components 

* **accept** arbitrary inputs \(called “**props**”\) and 
* **return** React **elements** describing what should appear on the screen.

{% tabs %}
{% tab title="Function component" %}
```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

```javascript
const element = <Welcome name="Sara" />;
```
{% endtab %}

{% tab title="Class Component" %}
```javascript
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```
{% endtab %}
{% endtabs %}

### Extracting Components <a id="extracting-components"></a>

Don’t be afraid to split components into smaller components.

{% tabs %}
{% tab title="Comment" %}
```javascript
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

accepts `author` \(an object\), `text` \(a string\), and `date` \(a date\) as props, and describes a comment on a social media website.

This component can be **tricky** to change because of all the nesting, and it is also hard to reuse individual parts of it. 
{% endtab %}

{% tab title="extracting Avartar" %}
```javascript
function Avatar(props) {
  return (
    <img className="Avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    />
  );
}
```

The `Avatar` doesn’t need to know that it is being rendered inside a `Comment`. This is why we have given its prop a more generic name: `user` rather than `author`.

We recommend naming props from the component’s own point of view rather than the context in which it is being used.
{% endtab %}

{% tab title="Simplified Comment" %}
```javascript
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <Avatar user={props.author} />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```
{% endtab %}

{% tab title="extracting UserInfo" %}
```javascript
function UserInfo(props) {
  return (
    <div className="UserInfo">
      <Avatar user={props.user} />
      <div className="UserInfo-name">
        {props.user.name}
      </div>
    </div>
  );
}
```
{% endtab %}

{% tab title="Better Comment" %}
```javascript
function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```
{% endtab %}
{% endtabs %}

### Props are readonly. \(Pure Function\)

{% tabs %}
{% tab title="Strict Rule" %}
React is pretty flexible but it has a **single** **strict** **rule**:

**All React components must act like pure functions with respect to their props.**
{% endtab %}

{% tab title="Pure" %}
Whether you declare a component [as a function or a class](https://reactjs.org/docs/components-and-props.html#function-and-class-components), it must never modify its own props. 

Consider this `sum` function:

```javascript
function sum(a, b) {
  return a + b;
}
```

Such functions are called _**"Pure"**_ because 

* they do not attempt to change their inputs, and 
* always return the same result for the same inputs.
{% endtab %}

{% tab title="Impure" %}
In contrast, this function is impure because it changes its own input:

```javascript
function withdraw(account, amount) {
  account.total -= amount;
}
```
{% endtab %}
{% endtabs %}

## 3. State and Lifecycle

**State** is similar to props, but 

* it is private and 
* fully controlled by the component.

### Lifecycle method

{% tabs %}
{% tab title="componentDidMount\(\)" %}
If we want to [set up a timer](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setInterval) whenever the `Clock` is rendered to the DOM for the first time. This is called “**mounting**” in React. 

`componentDidMount()` method runs after the component output has been rendered to the DOM. This is a good place to set up a timer. 

```javascript
componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
}
```

Note how we save the timer ID right on `this`.

While `this.props` is set up by React itself and `this.state` has a special meaning, you are free to add additional fields to the class manually if you need to store something that doesn’t participate in the data flow \(like a timer ID\).
{% endtab %}

{% tab title="componentWillUnmount\(\)" %}
If we also want to [clear that timer](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/clearInterval) whenever the DOM produced by the `Clock` is removed. This is called “**unmounting**” in React. In applications with many components, it’s very important to free up resources taken by the components when they are destroyed.

```javascript
componentWillUnmount() {
    clearInterval(this.timerID);
}
```
{% endtab %}
{% endtabs %}

#### Timer Example

{% tabs %}
{% tab title="Skeleton" %}
```javascript
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
  }

  componentWillUnmount() {
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```
{% endtab %}

{% tab title="Complete" %}
```javascript
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```
{% endtab %}

{% tab title="Recap" %}
#### Recap on what’s going on and the order in which the methods are called:

1. When `<Clock />` is passed to `ReactDOM.render()`, React calls the constructor of the `Clock` component. Since `Clock` needs to display the current time, it initializes `this.state` with an object including the current time. We will later update this state.
2. React then calls the `Clock` component’s `render()` method. This is how React learns what should be displayed on the screen. React then updates the DOM to match the `Clock`’s render output.
3. When the `Clock` output is inserted in the DOM, React calls the `componentDidMount()`lifecycle method. Inside it, the `Clock` component asks the browser to set up a timer to call the component’s `tick()` method once a second.
4. Every second the browser calls the `tick()` method. Inside it, the `Clock` component schedules a UI update by calling `setState()` with an object containing the current time. Thanks to the `setState()` call, React knows the state has changed, and calls the `render()` method again to learn what should be on the screen. This time, `this.state.date` in the `render()` method will be different, and so the render output will include the updated time. React updates the DOM accordingly.
5. If the `Clock` component is ever removed from the DOM, React calls the `componentWillUnmount()` lifecycle method so the timer is stopped.
{% endtab %}
{% endtabs %}

### 3 things to know about setState\(\)

{% tabs %}
{% tab title="1. Do Not Modify State Directly" %}
For example, this will not re-render a component:

```javascript
// Wrong
this.state.comment = 'Hello';
```

Instead, use `setState()`:

```javascript
// Correct
this.setState({comment: 'Hello'});
```

The only place where you can assign `this.state` is the constructor.
{% endtab %}

{% tab title="2. State Updates May Be Asynchronous" %}
React may batch multiple `setState()` calls into a single update for performance.

Because `this.props` and `this.state` may be updated **asynchronously**, you **should not rely on their values for calculating the next state**.

For example, this code may fail to update the counter:

```javascript
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});
```

To fix it, use a second form of `setState()` that accepts a function rather than an object. That function will receive 

* the previous state as the first argument, and 
* the props at the time the update is applied as the second argument:

```javascript
// Correct
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```

We used an [arrow function](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions) above, but it also works with regular functions:

```javascript
// Correct
this.setState(function(state, props) {
  return {
    counter: state.counter + props.increment
  };
});
```
{% endtab %}

{% tab title="3. State Updates are Merged" %}
When you call `setState()`, React merges the object you provide into the current state.

For example, your state may contain several independent variables:

```javascript
  constructor(props) {
    super(props);
    this.state = {
      posts: [],
      comments: []
    };
  }
```

Then you can update them independently with separate `setState()` calls:

```javascript
  componentDidMount() {
    fetchPosts().then(response => {
      this.setState({
        posts: response.posts
      });
    });

    fetchComments().then(response => {
      this.setState({
        comments: response.comments
      });
    });
  }
```

The merging is shallow, so `this.setState({comments})` leaves `this.state.posts`intact, but completely replaces `this.state.comments`.
{% endtab %}
{% endtabs %}

### The Data Flows Down <a id="the-data-flows-down"></a>

**State is often called local or encapsulated**. 

* Neither parent nor child components can know if a certain component is stateful or stateless.
  * It is not accessible to any component other than the one that owns and sets it.
* they shouldn’t care whether it is defined as a function or a class.

A component may choose to **pass** its **state down** as **props** to its child components:

```javascript
<h2>It is {this.state.date.toLocaleTimeString()}.</h2>
```

This also works for user-defined components:

```javascript
<FormattedDate date={this.state.date} />
```

The `FormattedDate` component would 

* receive the `date` in its props and 
* wouldn’t know whether it came from the `Clock`’s state, from the `Clock`’s props, or was typed by hand:

```text
function FormattedDate(props) {
  return <h2>It is {props.date.toLocaleTimeString()}.</h2>;
}
```

This is commonly called a “**top-down”** or **“unidirectional” data flow**. 

Any state is always owned by some specific component, and any data or UI derived from that state can only affect components “below” them in the tree.

If you imagine a component tree as a waterfall of props, each component’s state is like an additional water source that joins it at an arbitrary point but also flows down.

To show that all components are truly isolated, we can create an `App` component that renders three `<Clock>`s:

```text
function App() {
  return (
    <div>
      <Clock />
      <Clock />
      <Clock />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

Each `Clock` sets up its own timer and updates independently.

In React apps, whether a component is stateful or stateless is considered an implementation detail of the component that may change over time. You can use stateless components inside stateful components, and vice versa.

## 4. Handling Events



## 5. Conditional Rendering

## 6. Lists and Keys

## 7. Forms

## 8. Lifting State up

## 9. Composition vs. Inheritance

## 10. Thinking in React

 





