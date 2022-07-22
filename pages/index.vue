<template>
<main class="main">
  <adProduct :onSend='addToList'/>
  <Card
    v-for="(card, index) in cardsData"
    :key="index"
    :cardData="card"
  />
</main>
</template>

<script>
import adProduct from '~/components/adProduct.vue'
import Card from '~/components/Card.vue'

export default {
  name: 'IndexPage',
  components: {
    Card,
    adProduct
  },
  data () {
    return {
      cardsData: [
        {
          prodName: 'hello',
          prodDescription: '12',
          prodImgUrl: '23',
          prodPrice: '34'
        }
      ]
    }
  },
  methods: {
    addToList (data) {
      this.cardsData.push(data)
    }
  }
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
