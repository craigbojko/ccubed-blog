# Mapping over Objects in JS

Simple function to map over values within an object.
The following keeps the same object structure, simply mutating each property value with the supplied function:

```javascript
const mapObject = (object, mutator = () => ({})) => {
  const fromEntries = (iterable) => (
    [...iterable].reduce((obj, [key, val]) => {
      obj[key] = val
      return obj
    }, {})
  )

  return fromEntries(Object.entries(object).map(([key, unwrappedEntities]) =>
      ([key, mutator(unwrappedEntities)])
  ))
}
```

It is called like so:

```javascript
mapObject({ test: 123 }, (value) => (value + 456))
// { test: 579 }
```
