<template>
  <div>
    <!-- 模板读取ref数据时会自动读取.value -->
    <h1>{{ count }}</h1>
    <button @click="add">点击</button>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  props: {},
  // 在beforeCreate之前执行的回调函数，一般用来提供模板使用的响应式数据和函数(更新数据的函数),
  // 不能通过this来访问当前实例
  setup() {
    // 定义一个响应式ref对象
    const count = ref(0); //引用对象，内部包含了一个value属性来存储数据
    console.log(count);
    const add = () => {
      count.value += 1;
    };
    // 返回对象中的所有属性和方法，模板可以直接访问
    return { count, add };
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
