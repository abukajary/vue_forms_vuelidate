<template>
    <form class="user-info" @submit.prevent="sendAddrForm">
        <p>Форма вашего аддреса</p>
        <p>* - Обязательное поле для заполнения</p>

        <label for="index">Индекс</label>
        <input type="text" id="index"
               v-model.trim="post_index">

        <label for="country">Страна</label>
        <input type="text" id="country"
               v-model.trim="country">

        <label for="region">Область</label>
        <input type="text" id="region"
               v-model.trim="region">

        <label for="city">Город *</label>
        <input type="text" id="city"
               :class="$v.city.$error ? 'is-invalid' : ''"
               v-model="city">
        <p v-if="$v.city.$dirty && !$v.city.required"
           class="validator_err">Введите ваш город</p>

        <label for="street">Улица</label>
        <input type="text" id="street"
               v-model="street">

        <label for="apt">Дом</label>
        <input type="text" id="apt"
               v-model="apt">
        <label></label>
        <button type="submit">Отправить!</button>
    </form>
</template>

<script>
    import { validationMixin } from 'vuelidate'
    import { required } from 'vuelidate/lib/validators'
    export default {
        mixins: [validationMixin],
        data() {
            return {
                post_index: '',
                country: '',
                region: '',
                city: '',
                street: '',
                apt: '',  // apartments
            }
        },
        validations: {
            city: { required }
        },
        methods: {
            sendAddrForm() {
                this.$v.$touch()
                if (!this.$v.$error) {
                    document.getElementsByTagName('form')[1].classList.add('done')
                }
            }
        }
    }
</script>

<style lang="sass">
</style>