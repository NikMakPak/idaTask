<template>
  <div class="card">
    <button class="delete btn" @click="$emit('remove',id)">Удалить</button>
    <div class="card__content">
        <img :src="url" alt="">
        <h3 class="card__header">{{title}}</h3>
        <p class="card__description">{{desc}}</p>
        <p class="card__price">{{price}} Р</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardBlock',
  props: {
    title: {
      type: String,
      required: true
    },
    url: {
      type: String,
      required: true
    },
    desc: String,
    price: {
      type: String,
      required: true
    },
    id: Number
  }
}
</script>

<style>
.card{
animation: appear 1s;
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
