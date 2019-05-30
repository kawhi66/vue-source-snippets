```JavaScript
/**
 * @path src/core/instance/state.js
 */
 import config from '../config'
 import Watcher from '../observer/watcher'
 import Dep, { pushTarget, popTarget } from '../observer/dep'
 import { isUpdatingChildComponent } from './lifecycle'

 import {
   set,
   del,
   observe,
   defineReactive,
   toggleObserving
 } from '../observer/index'

 import {
   warn,
   bind,
   noop,
   hasOwn,
   hyphenate,
   isReserved,
   handleError,
   nativeWatch,
   validateProp,
   isPlainObject,
   isServerRendering,
   isReservedAttribute
 } from '../util/index'

 const computedWatcherOptions = { lazy: true }

 function initComputed (vm: Component, computed: Object) {
   // $flow-disable-line
   const watchers = vm._computedWatchers = Object.create(null)
   // computed properties are just getters during SSR
   const isSSR = isServerRendering()

   for (const key in computed) {
     const userDef = computed[key]
     const getter = typeof userDef === 'function' ? userDef : userDef.get
     if (process.env.NODE_ENV !== 'production' && getter == null) {
       warn(
         `Getter is missing for computed property "${key}".`,
         vm
       )
     }

     if (!isSSR) {
       // create internal watcher for the computed property.
       watchers[key] = new Watcher(
         vm,
         getter || noop,
         noop,
         computedWatcherOptions
       )
     }

     // component-defined computed properties are already defined on the
     // component prototype. We only need to define computed properties defined
     // at instantiation here.
     if (!(key in vm)) {
       defineComputed(vm, key, userDef)
     } else if (process.env.NODE_ENV !== 'production') {
       if (key in vm.$data) {
         warn(`The computed property "${key}" is already defined in data.`, vm)
       } else if (vm.$options.props && key in vm.$options.props) {
         warn(`The computed property "${key}" is already defined as a prop.`, vm)
       }
     }
   }
 }

 export function defineComputed (
  target: any,
  key: string,
  userDef: Object | Function
) {
  const shouldCache = !isServerRendering()
  if (typeof userDef === 'function') {
    sharedPropertyDefinition.get = shouldCache
      ? createComputedGetter(key)
      : createGetterInvoker(userDef)
    sharedPropertyDefinition.set = noop
  } else {
    sharedPropertyDefinition.get = userDef.get
      ? shouldCache && userDef.cache !== false
        ? createComputedGetter(key)
        : createGetterInvoker(userDef.get)
      : noop
    sharedPropertyDefinition.set = userDef.set || noop
  }
  if (process.env.NODE_ENV !== 'production' &&
      sharedPropertyDefinition.set === noop) {
    sharedPropertyDefinition.set = function () {
      warn(
        `Computed property "${key}" was assigned to but it has no setter.`,
        this
      )
    }
  }
  Object.defineProperty(target, key, sharedPropertyDefinition)
}

function createComputedGetter (key) {
  return function computedGetter () {
    const watcher = this._computedWatchers && this._computedWatchers[key]
    if (watcher) {
      if (watcher.dirty) {
        watcher.evaluate()
      }
      if (Dep.target) {
        watcher.depend()
      }
      return watcher.value
    }
  }
}

function createGetterInvoker(fn) {
  return function computedGetter () {
    return fn.call(this, this)
  }
}
```
