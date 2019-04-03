# Dumb Component vs. Smart Component

{% embed url="https://medium.com/@thejasonfile/dumb-components-and-smart-components-e7b33a698d43" %}

## Dumb Component \(Also, Known as Stupid Component, Presentational Component\)

* Their only responsibility is to present something to the DOM. 
  * Once that is done, the component is done with it. 
  * No keeping tabs on it, no checking in once in a while to see how things are going. Nope. 
  * Put the info on the page and move on.
* The components themselves **only** have a render\(\) method \(they don’t need any others\) 
* are often just Javascript functions. 
* don’t have internal state to manage. 
* wouldn’t know how to change the data they are presenting if they were asked. 
* The component can be written in one place and used several times throughout the app,
* each instance of that component will look the same. 
* If you want to change the look, you only have one place to go.

```javascript
const Footer = (props) => {
  return(
  <div>
    <ul>
      <li>Footer Information</li>
    </ul>
  </div>
  )
}
```

## Smart Component \(Or, Container Component\)

Smart components on the other hand have a different responsibility. 

* keep track of state and care about how the app works.

Using the **container design pattern**, 

* the container components are separated from the presentational components and each handles their own side of things. 
  * The container components do the heavy lifting and pass the data down to the presentational components as props.

They are class-based components and have their own state defined in their `constructor()` functions.

These components also often 

* contain other callback functions that are used to update the state and 
* get passed down to their child components as props.

The root component off an app is a good example of a smart component. It is often responsible for maintaining several pieces of state for the entire app and needs to pass down additional functions to its child components so that the state can be updated when a user interacts with the site.

```javascript
class App extends Component {
  constructor(props){
    super(props);
    this.state = {pictures : []};
  }
}
```

## 

## 

## 

## Pure Component

### Pure Component vs. Stateless component

