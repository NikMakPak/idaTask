<template>
<main class="main">
  <Add-product @onSend='addToList'/>
  <transition-group name="list">
    <card
      v-for="(card) in cardsData"
      :key="card.id"
      :title="card.prodName"
      :url="card.prodImgUrl"
      :price="card.prodPrice"
      :desc="card.prodDescription"
      :id="card.id"
      @remove="removeCard"
    />
  </transition-group>
</main>
</template>

<script>
import AddProduct from '~/components/AddProduct.vue'
import Card from '~/components/Card.vue'

export default {
  name: 'IndexPage',
  components: {
    Card,
    AddProduct
  },
  data () {
    return {
      cardsData: [
        {
          prodName: 'Наименование товара',
          prodDescription: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          prodImgUrl: 'https://avatars.mds.yandex.net/get-images-cbir/369811/6lYUqNpmw5HHtyFFqTpHjw7535/ocr',
          prodPrice: '10 000',
          id: Date.now()
        }
      ]
    }
  },
  methods: {
    addToList (data) {
      this.cardsData.push(data)
    },
    removeCard (id) {
      this.cardsData = this.cardsData.filter(el => el.id !== id)
    }
  }
}
</script>

<style lang="scss" scoped>
@import "@/assets/scss/variables";
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.main{
  display: flex;
  flex-wrap: wrap;
  padding: 32px;
  gap: 16px;
}
.list-item {
  display: inline-block;
  margin-right: 10px;
}
.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
