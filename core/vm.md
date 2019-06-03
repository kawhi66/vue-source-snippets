```JavaScript
vm._uid
vm._isVue
vm._renderProxy
vm._self
vm._watcher
vm._watchers
vm._computedWatchers
vm._inactive
vm._directInactive
vm._isMounted
vm._isDestroyed
vm._isBeingDestroyed
vm._events
vm._hasHookEvent
vm._vnode = null // the root of the child tree
vm._staticTrees = null // v-once cached trees
vm._props

// bind the createElement fn to this instance
// so that we get proper render context inside it.
// args order: tag, data, children, normalizationType, alwaysNormalize
// internal version is used by render functions compiled from templates
vm._c = (a, b, c, d) => createElement(vm, a, b, c, d, false)
// normalization is always applied for the public version, used in
// user-written render functions.
vm.$createElement = (a, b, c, d) => createElement(vm, a, b, c, d, true)

vm.$options
vm.$parent
vm.$root
vm.$children
vm.$refs
vm.$vnode // the placeholder node in parent tree
vm.$slots
vm.$scopedSlots
vm.$attrs // defineReactive
vm.$listeners // defineReactive
vm.$emit
```
