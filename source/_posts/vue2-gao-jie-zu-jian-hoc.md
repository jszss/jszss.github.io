---
title: 'Vue2 高阶组件 HOC'
date: 2021-06-30 11:21:47
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
// hoc.js
export default function EnhanceWrapper (WrappedComponent) {
  return {
    mounted () {
      console.log('I have already mounted')
    },
    props: WrappedComponent.props,
    render (h) {
      const slots = Object.keys(this.$slots)
        .reduce((arr, key) => arr.concat(this.$slots[key]), [])
        .map(vnode => {
          vnode.context = this._self
          return vnode
        })

      return h(WrappedComponent, {
        on: this.$listeners,
        props: this.$props,
        // 透传 scopedSlots
        scopedSlots: this.$scopedSlots,
        attrs: this.$attrs
      }, slots)
    }
  }
}

// 使用方式
import hoc from 'hoc.js'
import ElInput from 'Element-ui'
const HInput = hoc(ElInput)
 components: {
   HInput
 }
```