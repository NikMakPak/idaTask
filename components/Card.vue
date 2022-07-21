<template>
  <div class="card">
    <div class="delete btn"></div>
    <div class="card__content">
        <img src="@/static/product-img.png" alt="">
        <h3 class="card__header">Название</h3>
        <p class="card__description">Описание</p>
        <p class="card__price">100 p</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardBlock'
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
