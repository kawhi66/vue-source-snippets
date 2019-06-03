```JavaScript
/**
 * @path src/core/instance/events.js
 */
 Vue.prototype.$once = function (event: string, fn: Function): Component {
   const vm: Component = this
   function on () {
     vm.$off(event, on)
     fn.apply(vm, arguments)
   }
   on.fn = fn
   vm.$on(event, on)
   return vm
 }
```
