# React JS - Next JS 😇

Several methods for geting input field value.


## Option 1

``` javascript
class App extends React.Component {

  constructor(props) {
    super(props)
    this.state = { inputValue: '' }
  }

  foo(e) {
    this.setState({ inputValue: e.target.value })
  }

  bar() {
    console.log(this.state.inputValue)
  }

  render() {

    return (
      <div>
        <input onChange={(e) => this.foo(e)} />
        <button onClick={() => this.bar()}>Click</button>
      </div>
    )
  }
}
```

## Option 2

``` javascript
class App extends React.Component {

  constructor(props) {
    super(props)
    this.state = { inputValue: '' }
    // This binding is necessary to make `this` work in the callback
    this.foo = this.foo.bind(this);
    this.bar = this.bar.bind(this);
  }

  foo(e) {
    this.setState({ inputValue: e.target.value })
  }

  bar() {
    console.log(this.state.inputValue)
  }

  render() {

    return (
      <div>
        <input onChange={this.foo} />
        <button onClick={this.bar}>Click</button>
      </div>
    )
  }

}
```

##  Option 3
```javascript

function App() {

  const [inputValue, setValue] = useState('');

  const showValue = () => {
    console.log(inputValue)
  }

  return (
    <div>
      <input onChange={(e) => setValue(e.target.value)} />
      <button onClick={() => showValue()}>Click</button>
    </div>
  )
}
```
## Option 4

```javascript
const Input = props => {

  let refInput = React.createRef();

  function handler() {
    console.log(refInput.current.value)
  }

  return (
    <div>
      <input ref={refInput} />
      <button onClick={handler}>Click</button>
    </div>)

}
```

## Option 5

``` javascript
const Input = props => {

  return (
    <div>
      <input onChange={props.changeValue} />
      <button onClick={props.showValue}>Click</button>
    </div>)

}

class App extends React.Component {

  constructor(props) {
    super(props)
    this.state = { inputValue: '' }
  }

  changeValue = event => {
    this.setState({ inputValue: event.target.value })
  }

  showValue = () => {
    console.log(this.state.inputValue)
  }

  render() {
    return (
      <div>
        <Input changeValue={this.changeValue} showValue={this.showValue} />
      </div>
    )
  }
}


```