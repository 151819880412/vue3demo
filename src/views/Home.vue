<template>
  <div class="home">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import { defineComponent } from 'vue'
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

// export default {
//   name: 'Home',
//   components: {
//     HelloWorld
//   }
// }

export default defineComponent({
  name:'Home',
  components:{
    HelloWorld
  }
})

</script>
