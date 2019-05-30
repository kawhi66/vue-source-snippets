```JavaScript
/**
 * @path src/core/instance/events.js
 */
 import { updateListeners } from '../vdom/helpers/index'
 
 export function initEvents (vm: Component) {
   vm._events = Object.create(null)
   vm._hasHookEvent = false
   // init parent attached events
   const listeners = vm.$options._parentListeners
   if (listeners) {
     updateComponentListeners(vm, listeners)
   }
 }

 export function updateComponentListeners (
  vm: Component,
  listeners: Object,
  oldListeners: ?Object
) {
  target = vm
  updateListeners(listeners, oldListeners || {}, add, remove, createOnceHandler, vm)
  target = undefined
}
```
