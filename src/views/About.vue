<template>
    <div>

    </div>
</template>

<script>
export default {
    props: {

    },
    setup() {
      /**
       * 生命周期函数：
       *    1.vue3将 beforeDestroy 和 destroyed 改为 beforeUnmount 和 unmounted
       *    2.选项API生命周期选项和组合API之间的映射
       *        beforeCreate   ->setup 代替
       *        created        ->setup 代替
       *        beforeMount    ->onBeforeMount
       *        mounted        ->onMounted
       *        beforeUpdate   ->onBeforeUpdate
       *        update         ->onUpdate
       *        beforeUnmount  ->onBeforeUnmount
       *        unmounted      ->onUnmounted
       *        //用于处理错误
       *        errorCaptures  ->onErrorCaptures
       *        //新增的专门用于调试
       *        renderTracked  ->onRenderTracked 
       *        renderTriggered->onRenderTriggered
       *    3.vue3提供两套生命周期，一套写在组合API中，一套和
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

    },
    watch: {

    },
    methods: {

    },
    components: {

    },
};
</script>

<style>

</style>
