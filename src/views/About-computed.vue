<template>
  <div>
    <!-- 模板读取ref数据时会自动读取.value -->
    <h1>count:{{ count }}</h1>
    <h1>double:{{ double }}</h1>
    <h1>double2:{{ double2 }}</h1>
    <button @click="add">点击</button>
  </div>
</template>

<script>
import { ref , computed } from "vue";
export default {
  props: {},
  // 在beforeCreate之前执行的回调函数，一般用来提供模板使用的响应式数据和函数(更新数据的函数),
  // 不能通过this来访问当前实例
  setup() {
    // 定义一个响应式ref对象
    const count = ref(0); //引用对象，内部包含了一个value属性来存储数据

    // 计算属性：getter
    const double = computed(()=>{
      return count.value*2
    })
    // 计算属性：getter&&setter
    const double2 = computed({
      get(){
        return count.value*2
      },
      set(value){
        count.value += 1
      }
    })


    const add = () => {
      count.value += 1;
      setTimeout(()=>{
        double2.value+=2
      },2000)
    };

    // 返回对象中的所有属性和方法，模板可以直接访问
    return { count, add , double, double2 };
  },
  data() {
    return {};
  },
  computed: {},
  created() {},
  mounted() {},
  watch: {},
  methods: {},
  components: {},
};
</script>

<style scoped rel="stylesheet/stylus" lang="stylus"></style>
