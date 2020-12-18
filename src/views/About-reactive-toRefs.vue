<template>
    <div>
      <h1>msg:{{state.msg}}</h1>
      <h1>numbers:{{state.numbers}}</h1>
      <h1>person:{{state.person}}</h1>
      <button @click="state.update">点击</button>
      <h1>msg:{{msg}}</h1>
      <h1>numbers:{{numbers}}</h1>
      <h1>person:{{person}}</h1>
      <button @click="update">点击</button>
    </div>
</template>

<script>
/**
 * reactive：将复杂对象包装成响应式数据
 *           包装的方法在HTML中需要加前缀
 *           一旦结构出来的属性就不是响应式的了
 * toRefs：将对象的每个属性都变为ref对象(ObjectRefImpl)
 */
import {reactive,toRefs} from 'vue'
export default {
    props: {

    },
    setup() {
      // state对象是reactive中原始对象的代理对象，一旦操作代理对象的属性，内部操作的是原始对象的属性
      let state = reactive({
        msg:'abc',
        numbers:[1,2,3],
        person:{
          name:'tom'
        },
        update:()=>{
          state.msg += '--'
          state.numbers[0] += 1           //在vue2中不会自动更新，在vue3中会自动更新
          state.person.name = 'xiaoming'
          state.person.age = 18
        }
      })

      let state1 = reactive({
        msg:'abc',
        numbers:[1,2,3],
        person:{
          name:'tom'
        },
        update:()=>{
          // 问题：reactive响应式对象一旦结构出来的属性就不是响应式的了
          // 解决：将对象的每个属性都变为ref对象
          state1.msg += '--'
          state1.numbers[0] += 1
          state1.person.name += '-'

          // 还是响应式--会自动更新
          // state1.numbers[0] += 1           //在vue2中不会自动更新，在vue3中会自动更新
          // state1.person.name += '-'
          // state1.person.age += '1'
        }
      })
      let stateRef = toRefs(state1)   //将对象的每个属性都变为ref对象
      console.log(stateRef)
      return{state,...stateRef}

    },
    data() {
        return {

        };
    },
    computed: {

    },
    created() {

    },
    mounted() {

    },
    watch: {

    },
    methods: {

    },
    components: {

    },
};
</script>

<style scoped rel="stylesheet/stylus" lang="stylus">

</style>
