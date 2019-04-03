# Learn React in 5 min



{% embed url="https://medium.freecodecamp.org/learn-react-js-in-5-minutes-526472d292f4" caption="" %}

## Starting Point \(Index.js and index.html\)

{% tabs %}
{% tab title="Index.html" %}
```markup
<html> 
  <head>
    <script src="https://unpkg.com/react@15/dist/react.min.js"> </script>
    <script src="https://unpkg.com/react-dom@15/dist/react-dom.min.js"> </script>
    <script src="https://unpkg.com/babel-standalone@6.15.0/babel.min.js"></script>
  </head>
<body>
  <div id="root"></div>
  <script type="text/babel">  
    /* 
    ADD REACT CODE HERE 
    */
  </script>
</body>
</html>
```
{% endtab %}

{% tab title="index.js \(ReactDOM\)" %}
```javascript
ReactDOM.render(
    <Hello message="my friend" />, 
    document.getElementById("root")
);
```
{% endtab %}
{% endtabs %}

## React Component and Props

{% tabs %}
{% tab title="Component receiving props" %}
```javascript
class Hello extends React.Component {
    render() {
        return <h1>Hello world! {this.props.message}!</h1>;
    }
}
```
{% endtab %}

{% tab title="Component sending props" %}
```javascript
ReactDOM.render(
    <Hello message="my friend" />, 
    document.getElementById("root")
);
```
{% endtab %}
{% endtabs %}

## React Component States

{% tabs %}
{% tab title="Initializing State" %}
```javascript
class Hello extends React.Component {
   constructor(){
        super()
        this.state = {
            message: "my friend (from state)!"
        }
   }
}   
```

* `this.state = {`  inside the constructor initializes state
  * Before we set the state, we have to call `super()` in the constructor. 
    * This is because `this` is uninitialized before `super()` has been called.
{% endtab %}

{% tab title="Updating State" %}
```javascript
class Hello extends React.Component {
   constructor(){
        super()
        this.state = {
            message: "my friend (from state)!"
        }
        this.updateMessage = this.updateMessage.bind(this)
   }
   updateMessage() {
        this.setState({
            message: "my friend (from changed state)!"
        })
   } 
}
```

* To modify state, we call `this.setState({})` , passing in the new state object as the argument.
* In order to use `this` in other method, such as `updateMessage()`, we also need to `bind` method with `this` in constructor.

```javascript
this.updateMessage = this.updateMessage.bind(this)
```
{% endtab %}

{% tab title="Using the State" %}
```javascript
class Hello extends React.Component {
    constructor(){
        super();
        this.state = {
            message: "my friend (from state)!"
        };
        this.updateMessage = this.updateMessage.bind(this);
    }
    updateMessage() {
        this.setState({
            message: "my friend (from changed state)!"
        });
    }
    render() {
        return (
           <div>
             <h1>Hello {this.state.message}!</h1>
             <button onClick={this.updateMessage}>Click me!</button>
           </div>   
        )
    }
}    
```
{% endtab %}
{% endtabs %}



