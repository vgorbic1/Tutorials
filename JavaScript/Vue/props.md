## Props

### Props Validation
To make sure that you receive allowed type of data, use a validation on the props. To make the props suitable for validation, instead of
an array of props use an object, where each prop is a key and the type of props is value. You also may allow to get a multiple types, if
the value set to an array. Besides, the value itself also may be an object. The first key of such object will be the type, the second is
metadata such as requirement of this prop.

Simple props declaration:
```
props: ['name']
```
Props with type validation:
```
props: {
  name: String,
  age: [String, Array]
}
```
Props with metadata validation:
```
props: {
  name: {
    type: String,
    required: true
  }
}
```
Props with validation of seveal types and metadata:
```
props: {
  name: {
    type: Array,
    default: funciont() {
      name: 'Vlad'
    }
  }
}
```
