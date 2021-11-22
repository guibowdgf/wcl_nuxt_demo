<template>
  <div>
    <p> {{$route.path}}</p>
    <ul v-for="item in items"
        :key="item.id">
      <li>{{item.name+ $route.params.content.name +"的年龄是： "+$route.params.content.age+"岁"}}</li>
    </ul>
    <nuxt-link to="/newpage">
      <p class="link">回到newpage</p>
    </nuxt-link>
  </div>
</template>

<script>
export default {
  async asyncData (params) {
    console.log("ContentTest Params: " + params);
  },
  data () {
    return {
      items: [{ name: '測試1 ', id: 0 }, { name: '測試2 ', id: 1 }],
    }
  }
}
</script>
<style scoped>
p.link {
  color: bisque;
}
</style>