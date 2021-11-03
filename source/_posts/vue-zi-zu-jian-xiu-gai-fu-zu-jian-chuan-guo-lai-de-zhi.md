---
title: 'Vue 子组件修改父组件传过来的值'
date: 2019-09-27 14:46:10
tags: [Vue]
published: false
hideInList: false
feature: 
---
v-model在使用的时候很像双向绑定的，但是 Vue 是单项数据流，v-model 只是语法糖而已：父组件用v-bind将值传给子组件，子组件通过 change/input 事件触发修改父组件的值。
```
<input v-model="inputValue" />
<!-- 等价于 -->
<input :value="inputValue" @change="inputValue = $event.target.value" />
```
v-model 不仅仅能在 input 上用，在组件上也能使用。

vue 组件间传递数据是单向的，即数据总是由父组件传递到子组件，子组件在其内部可以有自己维护的数据，但它无权修改父组件传递给它的数据，我们也可以参照v-model语法糖进行修改父组件的值，但是每次都这样写太麻烦了，vue 提供了一个修饰符.sync,用法如下：
```
<child :value.sync="inputValue"></child>
<!-- 子组件 -->
<script>
export default {
    props: {
        //props可以设置值得类型，默认值，是否必传以及校验函数
        value: {
            type: [String, Number],
            required: true,
        },
    },
    //用一个变量中转，子组件中就用_value就不会直接修改父组件的值
    computed: {
        _value: {
            get() {
                return this.value;
            },
            set(val) {
                this.$emit('update:value', val);
            },
        },
    },
};
</script>
```