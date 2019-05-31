```JavaScript
/**
 * @path src/core/instance/render.js
 */
 import {
  nextTick
} from '../util/index'

 Vue.prototype.$nextTick = function (fn: Function) {
   return nextTick(fn, this)
 }
```
