<template>
    <aside class="wrapper">
        <h2>Добавление товара</h2>
        <ul>
          <li v-for="(el,i) in notValid"
          :key="i">{{el}} is not valid</li>
        </ul>
        <form class="form" @submit.prevent="sendData" @input="validCheck">
            <div class="form__item">
                <label for="prodName" class="form__label required">Наименование товара</label>
                <input v-model="formData.prodName"
                    type="text"
                    name="prodName"
                    id="prodName"
                    required
                    class="form__input"
                    placeholder="Введите наименование товара">
            </div>
            <div class="form__item">
                <label for="prodDescription" class="form__label">Описание товара</label>
                <textarea v-model="formData.prodDescription"
                name="prodDescription"
                id="prodDescription"
                cols="30"
                rows="10"
                class="form__input"
                placeholder="Введите описание товара"></textarea>
            </div>
            <div class="form__item">
                <label for="prodImgUrl" class="form__label required">Ссылка на изображение товара</label>
                <input v-model="formData.prodImgUrl"
                    type="url"
                    name="prodImgUrl"
                    id="prodImgUrl"
                    required
                    class="form__input"
                    placeholder="Введите ссылку">
            </div>
            <div class="form__item">
                <label for="prodPrice" class="form__label required">Цена товара</label>
                <input v-model="formData.prodPrice"
                    @input="formatPrice"
                    type="text"
                    name="prodPrice"
                    id="prodPrice"
                    required
                    class="form__input"
                    placeholder="Введите цену">
            </div>
            <button type="submit" class="form__btn" :disabled="!isFormValid">Добавить товар</button>
        </form>
    </aside>
</template>

<script>
// TODO: выделить кпоку на компонент. туда перенести js/ сделать валидацию
export default {
  name: 'AddProduct',
  props: ['onSend'],
  data () {
    return {
      formData: {
        prodName: '',
        prodDescription: '',
        prodImgUrl: '',
        prodPrice: '',
        id: ''
      },
      isFormValid: false,
      notValid: []
    }
  },
  methods: {
    sendData () {
      this.$emit('onSend', {
        prodName: this.formData.prodName,
        prodDescription: this.formData.prodDescription,
        prodImgUrl: this.formData.prodImgUrl,
        prodPrice: this.formData.prodPrice,
        id: Date.now()
      })
      for (const item in this.formData) {
        this.formData[item] = ''
      }
    },
    validCheck () {
      this.notValid = []
      for (const item in this.formData) {
        if (this.formData[item] === '') {
          if (item !== 'prodDescription' && item !== 'id') {
            this.notValid.push(item)
          }
        }
      }
      if (this.notValid.length === 0) {
        this.isFormValid = true
      } else {
        this.isFormValid = false
      }
    },
    formatPrice () {
      if (this.formData.prodPrice < 0) {
        this.formData.prodPrice = 0
        return
      }
      if (this.formData.prodPrice.replace(/\s/g, '').length > 3) {
        const price = parseInt(this.formData.prodPrice.replace(/\s/g, ''))
        this.formData.prodPrice = price.toLocaleString('ru-RU')
      } else {
        this.formData.prodPrice = this.formData.prodPrice.replace(/\s/g, '')
      }
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
</style>
