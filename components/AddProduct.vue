<template>
    <aside class="wrapper">
        <h2>Добавление товара</h2>
        <ul v-if="notValid.length > 0">
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
                rows="5"
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
            <button type="submit" class="btn" :disabled="!isFormValid">Добавить товар</button>
        </form>
    </aside>
</template>

<script>
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
      this.isFormValid = false
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

<style lang="scss" scoped>
@import "@/assets/scss/variables";
label.required:after
{
    content: "\2022";
    color: red;
    font-size: 24px;
}
.form{
  background: $card-bg;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  padding: 24px;
  max-width: 332px;
  margin-top: 16px;
}
h2{
  font-weight: 600;
  font-size: 28px;
  margin: 0;
}
.form__label{
  font-weight: 400;
  font-size: $form-label-font;
  letter-spacing: -0.02em;
}
.form__item{
  margin-bottom: 16px;
}
input, textarea{
  color: #B4B4B4;
  background: $card-bg;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  padding: 10px 0 10px 16px;
}
button{
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@600&display=swap');
  margin-top: 8px;
  background: #28D62F;
  border-radius: 10px;
  padding: 10px 95px;
}
button[disabled]{
  background: #EEEEEE;
  pointer-events: none;
}
</style>
