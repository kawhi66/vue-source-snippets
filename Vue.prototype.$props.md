```JavaScript
/**
 * @path src/core/instance/state.js
 */
const propsDef = {}
propsDef.get = function () { return this._props }
if (process.env.NODE_ENV !== 'production') {
  propsDef.set = function () {
    warn(`$props is readonly.`, this)
  }
}
Object.defineProperty(Vue.prototype, '$props', propsDef)
```
