<template>
    <aside class="wrapper">
        <h2>Добавление товара</h2>
        <form class="form" @submit.prevent="addCard">
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
                    type="number"
                    name="prodPrice"
                    id="prodPrice"
                    required
                    class="form__input"
                    placeholder="Введите цену">
            </div>
            <button v-on:click="addCart" type="submit" class="form__btn">Добавить товар</button>
        </form>
    </aside>
</template>

<script>
export default {
  name: 'AddProduct',
  data () {
    return {
      formData: {
        prodName: '',
        prodDescription: '',
        prodImgUrl: '',
        prodPrice: ''
      }
    }
  },
  methods: {
    addCard () {
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
