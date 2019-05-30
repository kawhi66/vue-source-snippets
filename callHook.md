```JavaScript
/**
 * @path src/core/instance/lifecycle.js
 */
 import {
  warn,
  noop,
  remove,
  emptyObject,
  validateProp,
  invokeWithErrorHandling
} from '../util/index'

 export function callHook (vm: Component, hook: string) {
   // #7573 disable dep collection when invoking lifecycle hooks
   pushTarget()
   const handlers = vm.$options[hook]
   const info = `${hook} hook`
   if (handlers) {
     for (let i = 0, j = handlers.length; i < j; i++) {
       invokeWithErrorHandling(handlers[i], vm, null, vm, info)
     }
   }
   if (vm._hasHookEvent) {
     vm.$emit('hook:' + hook)
   }
   popTarget()
 }
```
