```JavaScript
/**
 * @path src/core/instance/state.js
 */
 Vue.prototype.$watch = function (
   expOrFn: string | Function,
   cb: any,
   options?: Object
 ): Function {
   const vm: Component = this
   if (isPlainObject(cb)) {
     return createWatcher(vm, expOrFn, cb, options)
   }
   options = options || {}
   options.user = true
   const watcher = new Watcher(vm, expOrFn, cb, options)
   if (options.immediate) {
     try {
       cb.call(vm, watcher.value)
     } catch (error) {
       handleError(error, vm, `callback for immediate watcher "${watcher.expression}"`)
     }
   }
   return function unwatchFn () {
     watcher.teardown()
   }
 }
```
