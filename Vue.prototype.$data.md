```JavaScript
/**
 * @path src/core/instance/state.js
 */
 const dataDef = {}
 dataDef.get = function () { return this._data }
 if (process.env.NODE_ENV !== 'production') {
  dataDef.set = function () {
    warn(
      'Avoid replacing instance root $data. ' +
      'Use nested data properties instead.',
      this
    )
  }
}
 Object.defineProperty(Vue.prototype, '$data', dataDef)
```
