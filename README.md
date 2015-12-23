`redux-toastr` is a toastr message implemented with [Redux](https://github.com/rackt/redux), primary consists of three things: a Redux reducer, `redux-toastr` toastr emitter and a React component.

The reducer listens to dispatched actions from the component to maintain your state in Redux.
`redux-toastr` [demo](http://diegoddox.github.io/redux-toastr/)

## Implementation Guide

#### 1. Install redux-toastr

`npm install --save redux-toastr`

##### 2. Link `redux-toastr` styles to your app
#####NOTE: This can be changed at anytime
```
<link href="http://diegoddox.github.io/redux-toastr/0.3.0/redux-toastr.min.css" rel="stylesheet" type="text/css">
```
##### 3. The third thing you need to do is to add the `redux-toastr` reducer to Redux.

```
import {createStore, combineReducers} from 'redux'
import {reducer as toastrReducer} from 'redux-toastr'
const reducers = {
  // ... other reducers ...
  toastr: toastrReducer     // <---- Mounted at toastr.
}
const reducer = combineReducers(reducers)
const store = createStore(reducer)
```

##### NOTE: The default mount point for `redux-toastr` is `toastr`.

##### 4. Add the `redux-toastr` React component to the root of your app

```
import ReduxToastr from 'redux-toastr'
<Provider store={store}>
  <div>
    ... other things like router ...
    <ReduxToastr/>
  </div>
</Provider>
```

##### 5. Add the `toastr` 
The toastr method use [eventemitter3](https://github.com/primus/eventemitter3) to dispatch the actions

```
import React, {Component}  from 'react'
import {toastr} from 'redux-toastr'

export class YourComponent extends Component {
  render() {
    return (
      <div>
        <button
          onClick={() => toastr.success('The title', 'The message')}
          type="button">Toastr Success</button>
      </div>
    )
  }
}
```
Or you can bind the `actions` to your component if you prefer.
```
import {bindActionCreators} from 'redux'
import {actions as toastrActions} from 'redux-toastr'
// In your React component
constructor(props) {
  super(props);
  // Bind the redux-toastr actions to the component
  this.toastr = bindActionCreators(toastrActions, this.props.dispatch)
}
```
## Toastr method
`success` `info` `warning` `error`
Each method can take up to three arguments.

1. Passing three arguments the first is the `title` the second `message` and the third is the `options`
2. Passing two `string` arguments the first will be the `title` and the second the `message`
3. You can pass the `message` and the second argument can be the `options`
4. If you pass only one argument it will become the message 

| Title     |message     | options   |
| ----------|:----------:| ---------:|
| `string`  | `string`   | `object`  |

```
import {toastr} from 'redux-toastr'

const toastrOptions = {
  timeOut: number,
  onShowComplete: func, // <-- When the animation-show is complete
  onHideComplete: func, // <-- When the animation-hide is complete
  icon: string // Custom icon
}

toastr.success('Title', 'Message', toastrOptions)
toastr.info('The message', toastrOptions)
toastr.warning('The title', 'The message')
toastr.error('The message'})
```

##### Toastr icons
By default `redux-toastr` provides a icon for `success`, `info`, `warning` and `error`
but you can override by passing a object `{icon: 'icon-name'}` to the `toastr` method.

# Run a local demo
```
git clone https://github.com/diegoddox/redux-toastr.git
cd redux-toastr/demo/
npm install
npm start
```
open your browser at `http://localhost:3000`

# TODO
create test.