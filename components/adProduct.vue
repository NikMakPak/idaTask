<template>
    <aside class="wrapper">
        <h2>Добавление товара</h2>
        <form class="form" @submit.prevent="sendData">
            <div class="form__item">
                <label for="prodName" class="form__label required">Наименование товара</label>
                <input v-model="prodName"
                    type="text"
                    name="prodName"
                    id="prodName"
                    required
                    class="form__input"
                    placeholder="Введите наименование товара">
            </div>
            <div class="form__item">
                <label for="prodDescription" class="form__label">Описание товара</label>
                <textarea v-model="prodDescription"
                name="prodDescription"
                id="prodDescription"
                cols="30"
                rows="10"
                class="form__input"
                placeholder="Введите описание товара"></textarea>
            </div>
            <div class="form__item">
                <label for="prodImgUrl" class="form__label required">Ссылка на изображение товара</label>
                <input v-model="prodImgUrl"
                    type="url"
                    name="prodImgUrl"
                    id="prodImgUrl"
                    required
                    class="form__input"
                    placeholder="Введите ссылку">
            </div>
            <div class="form__item">
                <label for="prodPrice" class="form__label required">Цена товара</label>
                <input v-model="prodPrice"
                    type="number"
                    name="prodPrice"
                    id="prodPrice"
                    required
                    class="form__input"
                    placeholder="Введите цену">
            </div>
            <button type="submit" class="form__btn"">Добавить товар</button>
        </form>
    </aside>
</template>

<script>
// TODO: выделить кпоку на компонент. туда перенести js/ сделать валидацию
export default {
  name: 'adProduct',
  props: ['onSend'],
  data () {
    return {
      formValid: false,
      prodName: '',
      prodDescription: '',
      prodImgUrl: '',
      prodPrice: 0,
      id: 0
    }
  },
  methods: {
    sendData () {
      this.$emit('onSend', {
        prodName: this.prodName,
        prodDescription: this.prodDescription,
        prodImgUrl: this.prodImgUrl,
        prodPrice: parseInt(this.prodPrice),
        id: Date.now()
      })
      this.prodName = this.prodDescription = this.prodImgUrl = ''
      this.prodPrice = this.id = 0
    }
  }
}

</script>

<style lang="scss">
label.required:after
{
    content: "\2022";
    color: red;
    font-size: 24px;
}
input{
    display: block;
}
.form__btn{

}
</style>
