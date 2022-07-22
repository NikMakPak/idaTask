<template>
  <div class="card">
    <div class="delete btn"></div>
    <div class="card__content">
        <img src="@/static/product-img.png" alt="">
        <h3 class="card__header">{{cardData.prodName}}</h3>
        <p class="card__description">{{cardData.prodDescription}}</p>
        <p class="card__price">{{cardData.prodPrice}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardBlock',
  props: ['cardData']
}

</script>

<style>
.card{
animation: appear 3s;
}

@keyframes appear {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>
