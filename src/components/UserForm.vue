<template>
  <form class="user-info" id="userFom" @submit.prevent="sendForm">
    <p>Форма оснвной информации</p>
    <p>* - Обязательное поле для заполнения</p>

    <label for="lastName">Фамилия *</label>
    <input type="text" id="lastName"

           v-model.trim="form.last_name">
    <p v-if="$v.form.last_name.$dirty && !$v.form.last_name.required"
       class="validator_err">Введите свою фамилию</p>

    <label for="firstName">Имя *</label>
    <input type="text" id="firstName"
           v-model.trim="form.first_name">
    <p v-if="$v.form.first_name.$dirty && !$v.form.first_name.required"
       class="validator_err">Введите свое имя</p>

    <label for="middleName">Отчество</label>
    <input type="text" id="middleName"
           v-model.trim="form.middle_name">

    <label for="bornDate">Дата рождения *</label>
    <input type="date" id="bornDate"
           v-model="form.born_date" min="1900-01-01" max="2021-01-01">
    <p v-if="$v.form.born_date.$dirty && !$v.form.born_date.required"
       class="validator_err">Введи вашу дату рождения(месяц/день/год)</p>

    <label for="phoneNumber">Номер телефона *</label>
    <input type="tel" id="phoneNumber" maxlength="11" placeholder="7 --- --- -- --"
           v-model="form.phone_number">
    <p v-if="$v.form.phone_number.$dirty && !$v.form.phone_number.required"
       class="validator_err">Номер мобильного телефона начинся с 7</p>

    <label>Пол</label>
    <div class="form__gender">
      <div class="gender">
        <input type="radio" name="radioMale" id="male" value="Male"
               v-model="form.gender">
        <label for="male">Мужчина</label>
      </div>
      <div class="gender">
        <input type="radio" name="radioFemale" id="female" value="Female"
               v-model="form.gender">
        <label for="female">Женщина</label>
      </div>
    </div>

    <label for="customer_group_type">Группа клиентов *</label>
    <select id="customer_group_type" name="customer_group_type"
            v-model="form.customer_group" multiple>
      <option v-for="(group, index) in customer_group_type"
              :value="group.value"
              :key="index">
        {{ group.label }}
      </option>
    </select>
    <p v-if="$v.form.customer_group.$dirty && !$v.form.customer_group.required"
       class="validator_err">Выберите свою группу</p>

    <label for="therapist">Лечащий врач</label>
    <select id="therapist" name="therapist"
            v-model="form.dr">
      <option v-for="(dr, index) in therapists"
              :value="dr.value"
              :key="index">
        {{ dr.label }}
      </option>
    </select>

    <label for="isSms">Напомнить через СМС?</label>
    <label class="container">
      <input type="checkbox" id="isSms"
             v-model="form.sendSms">Напомните мне через смс!
    </label>
    <button type="submit">Отправить!</button>
  </form>
</template>

<script>
  import { validationMixin } from 'vuelidate'
  import {minLength, required} from 'vuelidate/lib/validators'
  export default {
    mixins: [validationMixin],
    data() {
      return {
        form: {
          last_name: '',
          first_name: '',
          middle_name: '',
          dr: '',
          customer_group: [],
          sendSms: false,
          gender: '',
          phone_number: '',
          born_date: ''
        },
        therapists: [
          {
            label: 'Иванов',
            value: 'Ivanov'
          },
          {
            label: 'Захаров',
            value: 'Zaharov'
          },
          {
            label: 'Чернышева',
            value: 'Chernysheva'
          },
        ],
        customer_group_type: [
          {
            label: 'VIP',
            value: 'VIP'
          },
          {
            label: 'Проблемные',
            value: 'isProblem'
          },
          {
            label: 'ОМС',
            value: 'isNecessarilyHasInsurance'
          },
        ],
      }
    },
    validations: {
      form: {
        last_name: { required },
        first_name: { required },
        born_date: { required },
        phone_number: { required, minLength: minLength(11) },
        customer_group: { required },
      }
    },
    methods: {
      sendForm() {
        this.$v.form.$touch()
        if (!this.$v.form.$error) {
          document.getElementById('userFom').classList.add('done')
        }
      }
    }
  }
</script>

<style lang="sass">
  body
    padding: 0
    margin: 0
    background: #f5f5f5

  form
    min-width: 365px
    display: flex
    justify-content: center
    flex-direction: column
    background: #0d0735
    padding: 30px
    margin: 20px
    color: white
    transition: opacity 1s linear
    opacity: 1

    p
      margin: 0
      padding: 0

    input
      height: 25px
      border: none
      background: #f5f5f5

    label
      padding: 5px 0
      margin: 5px 0

  .form__gender
    width: 100%
    display: flex
    justify-content: space-evenly
    align-items: center

    .gender
      input
        width: 12px
        height: 12px
        cursor: pointer

  .validator_err
    font-size: 15px
    color: red
    padding: 0
    margin: 0

  .container
    display: flex
    align-items: center

  button
    background: #f5f5f5
    height: 35px

  .done
    opacity: 0.3

    input
      pointer-events: none

    button
      display: none
</style>