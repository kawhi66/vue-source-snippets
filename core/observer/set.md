```JavaScript
 /**
  * Set a property on an object. Adds the new property and
  * triggers change notification if the property doesn't
  * already exist.
  */
 export function set (target: Array<any> | Object, key: any, val: any): any {
   if (process.env.NODE_ENV !== 'production' &&
     (isUndef(target) || isPrimitive(target))
   ) {
     warn(`Cannot set reactive property on undefined, null, or primitive value: ${(target: any)}`)
   }
   if (Array.isArray(target) && isValidArrayIndex(key)) {
     target.length = Math.max(target.length, key)
     target.splice(key, 1, val)
     return val
   }
   if (key in target && !(key in Object.prototype)) {
     target[key] = val
     return val
   }
   const ob = (target: any).__ob__
   if (target._isVue || (ob && ob.vmCount)) {
     process.env.NODE_ENV !== 'production' && warn(
       'Avoid adding reactive properties to a Vue instance or its root $data ' +
       'at runtime - declare it upfront in the data option.'
     )
     return val
   }
   if (!ob) {
     target[key] = val
     return val
   }
   defineReactive(ob.value, key, val)
   ob.dep.notify()
   return val
 }
```
