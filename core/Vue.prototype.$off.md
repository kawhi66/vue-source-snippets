```JavaScript
/**
 * @path src/core/instance/events.js
 */
 Vue.prototype.$off = function (event?: string | Array<string>, fn?: Function): Component {
   const vm: Component = this
   // all
   if (!arguments.length) {
     vm._events = Object.create(null)
     return vm
   }
   // array of events
   if (Array.isArray(event)) {
     for (let i = 0, l = event.length; i < l; i++) {
       vm.$off(event[i], fn)
     }
     return vm
   }
   // specific event
   const cbs = vm._events[event]
   if (!cbs) {
     return vm
   }
   if (!fn) {
     vm._events[event] = null
     return vm
   }
   // specific handler
   let cb
   let i = cbs.length
   while (i--) {
     cb = cbs[i]
     if (cb === fn || cb.fn === fn) {
       cbs.splice(i, 1)
       break
     }
   }
   return vm
 }
```
