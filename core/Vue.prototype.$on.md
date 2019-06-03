```JavaScript
/**
 * @path src/core/instance/events.js
 */
 const hookRE = /^hook:/
 Vue.prototype.$on = function (event: string | Array<string>, fn: Function): Component {
   const vm: Component = this
   if (Array.isArray(event)) {
     for (let i = 0, l = event.length; i < l; i++) {
       vm.$on(event[i], fn)
     }
   } else {
     (vm._events[event] || (vm._events[event] = [])).push(fn)
     // optimize hook:event cost by using a boolean flag marked at registration
     // instead of a hash lookup
     if (hookRE.test(event)) {
       vm._hasHookEvent = true
     }
   }
   return vm
 }
```
