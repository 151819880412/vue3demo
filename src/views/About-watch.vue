<template>
    <div>

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
import {reactive,toRefs,ref,watch} from 'vue'
export default {
    props: {

    },
    setup() {
      let count = ref(0)
      let state = reactive({
        msg:'abc',
        numbers:[1,2,3],
        person:{
          name:'tom'
        },
        update:()=>{
          state.msg += '--'
          state.numbers[0] += 1
          state.person.name += '-',
          count.value++
        }
      })
      let stateRef = toRefs(state)   //将对象的每个属性都变为ref对象
      console.log(stateRef)
      console.log(stateRef.numbers.value[0])

      // 监视一个ref
      watch(count,(newValue,oldValue)=>{
        console.log(newValue,oldValue)
        document.title = newValue
      })
      // 监视reactive对象中的某个属性：msg,//由于msg不是响应式数据，所以不能直接监视--1使用stateRef.msg--2使用函数返回他的getter
      watch(()=>state.msg,(newValue,oldValue)=>{
        console.log(newValue,oldValue)
      })
      // 监视多个数据,只能监视响应式的数据，否则会警告
      watch([count,()=>state.msg,stateRef.numbers.value],(values)=>{
        console.log(values)
      })

      return{...stateRef,count}

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
