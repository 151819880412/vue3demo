<template>
    <div>
      <input type="text" autocomplete="on">
      <input type="password" autocomplete="on" style="display:none">
      <input type="password" autocomplete="on">
      <button @click="qqq">11</button>
    </div>
</template>

<script>
export default {
    props: {

    },
    setup() {
      /**
          比较vue2和vue3的响应式
            1.vue2的响应式
              核心：
                对象：通过defineProperty对对象已有属性值的读取和修改进行拦截(监视/拦截)
                数组：通过重写数组更新数组一系列更新元素的方法来实现元素的修改的劫持
              问题：
                对象：直接添加新的属性或者删除已有属性，视图不会更新(defineProperty只能监视读和修改)
                数组：直接通过修改下标替换元素或者更新length，视图不会更新
            2.vue3的响应式
              核心
                通过Proxy(代理，负责拦截)，拦截对data任意属性的任意(13种)操作，包含属性的读写，属性的添加，属性的删除..
                通过Relect(反射，负责修改)，动态对被代理对象的相应属性进行特定的操作
       */

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
      let data = {
        a:1
      }
      let proxyObj = new Proxy(data,{
        // 拦截读取属性值
        get(target,property,receiver){
          /**
              target：  目标对象
              property：被获取的属性名
              receiver：Proxy或者继承Proxy的对象
           */
          console.log('get',target,property,receiver)
          // Reflect.get()方法与从 对象 (target[propertyKey]) 中读取属性类似，但它是通过一个函数执行来操作的。
          return Reflect.get(target,property,receiver)
          /**
              不用return target[property]的原因：如果obj的__proto__指向Proxy且obj上某个属性和被Proxy包装对象的属性相同时且被Proxy包装对象有get(){return this.xxx}会出现this指向问题
                let data = {
                  _name: "zky",
                  get name() {
                    // 此时this指向调用它的People
                    // 使用Reflect.get之后this指向Man
                        调用Man.name时经过了以下几步
                        被proxy拦截，调用handler.get
                        handler.get中传入的receiver参数指向调用者--Man
                        调用Reflect.get，由于target中的name指定了getter，Reflect.get自动将调用的getter函数的this绑定到receiver，也就是Man

                    console.log(this);
                    return this._name;
                  },
                };
                let People = new Proxy(data, {
                  get(target, prop, receiver) {
                    return target[prop];
                    // return Reflect.get(target,prop,receiver)
                  },
                });
                console.log(People);
                let Man = { _name: "zky_man" };
                Man.__proto__ = People; // Man继承People
                console.log(Man._name); // zky_man
                console.log(Man.name); // zky
           */
          // return target[property]
        },
        // 拦截设置属性值或者添加新属性
        set(target,property,value,receiver){
          /**
              target：  目标对象
              property  将被设置的属性名或Symbol
              value     新属性值
              receiver  通常是proxy本身,但handler的set方法也有可能在原型链上,或以其他方式被间接地调用(因此不一定是proxy本身)
           */
          console.log('set',target,property,value,receiver)
          // 修改被代理对象的对应属性值或者添加新属性
          return Reflect.set(target,property,value,receiver)
        },
        // 拦截删除属性
        deleteProperty(target,property){
          /**
              target：  目标对象
              property  待删除的属性名
           */
          console.log('deleteProperty',target,property)
          return Reflect.deleteProperty(target,property)
        }
      })
      console.log(proxyObj.a)
    },
    watch: {

    },
    methods: {
      qqq(){

      }
    },
    components: {

    },
};
</script>

<style scoped rel="stylesheet/stylus" lang="stylus">

</style>
