<template>
  <div class="card" @click="toggleBtnClass">
    <button ref="delete" class="delete btn" @click="$emit('remove',id)"></button>
        <div class="img__wrap">
          <img :src="url" alt="">
        </div>
    <div class="card__content">
        <h3 class="card__header">{{title}}</h3>
        <p class="card__description">{{desc}}</p>
        <p class="card__price">{{price}} руб.</p>
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
  },
  methods: {
    toggleBtnClass () {
      this.$refs.delete.classList.toggle('visible')
    }
  }
}
</script>

<style lang="scss" scoped>
@import "@/assets/scss/variables";
.card{
  cursor: pointer;
  transition: $anim-time - .5s;
  position: relative;
  animation: appear $anim-time;
  background: $card-bg;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  max-width: 332px;
  max-height: 423px;
  &:hover{
      box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.08), 0px 0px 10px rgba(0, 0, 0, 0.06);
}
}

@keyframes appear {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
.img__wrap{
    height: 200px;
    width: 100%;
    overflow: hidden;
    border-radius: 4px 4px 0px 0px;
  img{
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}
.card__content{
  padding: 16px 16px 24px;
}
.card__price{
  font-weight: 600;
  margin-top: 32px;
}
.card__description{
  margin-top: 16px;
}
.delete{
  display: none;
  position: absolute;
  right: -10px;
  top: -10px;
  background: center no-repeat url("@/assets/img/delete.svg") #FF8484;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  width: 32px;
  height: 32px;
}
.visible{
  display: block;
}
</style>
