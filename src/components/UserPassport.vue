<template>
    <form class="user-info" @submit.prevent="sendPassportForm">
        <p>Форма паспорта</p>
        <p>* - Обязательное поле для заполнения</p>

        <label for="document_type">Тип документа *</label>
        <select id="document_type" name="document_type"
                v-model="form.document_type">
            <option v-for="(type, index) in document_type"
                    :value="type.value"
                    :key="index">
                {{ type.label }}
            </option>
        </select>
        <p v-if="$v.form.document_type.$dirty && !$v.form.document_type.required"
           class="validator_err">Укажите тип своего документа</p>
        <label for="series">Серия</label>
        <input type="text" id="series"
               v-model.trim="form.series">

        <label for="document_number">Номер</label>
        <input type="text" id="document_number"
               v-model.trim="form.document_number">

        <label for="authority">Кем выдан</label>
        <input type="text" id="authority"
               v-model.trim="form.authority">

        <label for="date_of_issue ">Дата выдачи *</label>
        <input type="date" id="date_of_issue "
               v-model="form.date_of_issue" min="2000-01-01">
        <p v-if="$v.form.date_of_issue.$dirty && !$v.form.date_of_issue.required"
           class="validator_err">Укажите дату выдачи своего документа</p>

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
                form: {
                    document_type: '',
                    series: '',
                    document_number: '',
                    authority: '',
                    date_of_issue: ''
                },
                document_type: [
                    {
                        label: 'Паспорт',
                        value: 'passport'
                    },
                    {
                        label: 'Свидетельство о рождении',
                        value: 'birth_certificate '
                    },
                    {
                        label: 'Вод. удостоверение',
                        value: 'drivers_license '
                    },
                ],
            }
        },
        validations: {
            form: {
                document_type: { required },
                date_of_issue: { required },
            }
        },
        methods: {
            sendPassportForm() {
                this.$v.form.$touch()
                if (!this.$v.form.$error) {
                    document.getElementsByTagName('form')[2].classList.add('done')
                }
            }
        }
    }
</script>

<style lang="sass">

</style>