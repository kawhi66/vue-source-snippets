```JavaScript
/**
 * @path src/core/instance/lifecycle.js
 */
 Vue.prototype.$forceUpdate = function () {
   const vm: Component = this
   if (vm._watcher) {
     vm._watcher.update()
   }
 }
```
