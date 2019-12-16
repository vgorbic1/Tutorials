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
Action is something what user does (e.g., clicking button).

### Reducer
Reucer is a pure function that receives an input (the action) and creates an output (new state). Reducer is
a slice of the entire State. An app has multiple reducers that work with a particular segment of the App.
The Root Reducer represents entire App State. Root reducer sends updated State back to components via props.
