```JavaScript
/**
 * @path src/core/instance/events.js
 */
 import {
   tip,
   toArray,
   hyphenate,
   formatComponentName,
   invokeWithErrorHandling
 } from '../util/index'
 
 Vue.prototype.$emit = function (event: string): Component {
   const vm: Component = this
   if (process.env.NODE_ENV !== 'production') {
     const lowerCaseEvent = event.toLowerCase()
     if (lowerCaseEvent !== event && vm._events[lowerCaseEvent]) {
       tip(
         `Event "${lowerCaseEvent}" is emitted in component ` +
         `${formatComponentName(vm)} but the handler is registered for "${event}". ` +
         `Note that HTML attributes are case-insensitive and you cannot use ` +
         `v-on to listen to camelCase events when using in-DOM templates. ` +
         `You should probably use "${hyphenate(event)}" instead of "${event}".`
       )
     }
   }
   let cbs = vm._events[event]
   if (cbs) {
     cbs = cbs.length > 1 ? toArray(cbs) : cbs
     const args = toArray(arguments, 1)
     const info = `event handler for "${event}"`
     for (let i = 0, l = cbs.length; i < l; i++) {
       invokeWithErrorHandling(cbs[i], vm, args, vm, info)
     }
   }
   return vm
 }
```
