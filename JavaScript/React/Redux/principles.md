## Redux Principles
- Single source of truth (one state place for entire app)
- State is read only (new state is created after each action)
- Changes using pure functions (same output for any number iterations of the same input)

### The flow
action &rarr; root reducer &rarr; store &rarr; DOM changes

### Flux Pattern
Redux uses unidirectional data flow in **Flux Pattern**: *action &rarr; dispatcher &rarr; store &rarr; view*

which is better than complex **MVC Pattern**: *action &rarr; controller &rarr; multiple models &harr; multiple views*

### Action
Action is something what user does (e.g., clicking button). It sends to reducer a type and payload with data that should
be modified.
```
{
  type: string,
  payload: any
}
```

### Reducer
Reucer is a pure function that receives an input (the action) and creates an output (new state). Reducer is
a slice of the entire State. An app has multiple reducers that work with a particular segment of the App.
The Root Reducer represents entire App State. Root reducer sends updated State back to components via props.

First a reducer checks what type of data was sent with action. Then it updates the property that with data that
was passed as a payload from an action. Reducer passes that modified property as a prop back to the component.
```
const userReducer => (state, action) {
  switch (action.type) {
    case 'SET_CURRENT_USER':
      return {
        ...state,
        currentUser: action.payload
      };
    default:
      return state;
  }
}
```
