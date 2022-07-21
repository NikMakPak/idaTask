<template>
<main class="main">
  <addProduct />
  <Card />
</main>
</template>

<script>
import Card from '~/components/Card.vue'
export default {
  components: { Card },
  name: 'IndexPage'
}
</script>

<style lang="scss">
@import "@/assets/scss/variables";
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.main{
  display: flex;
  flex-wrap: wrap;
}
</style>
