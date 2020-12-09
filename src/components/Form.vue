<template>
  <div class="forms-container">
      <Cover v-if="formComplete"/>
      <form class="form" @submit.prevent="formCheck">
        <div class="form-group input-form">
            <span>Фамилия</span>
            <input type="text" placeholder="Иванов" class="input" v-model.trim="form.secondName">
            <p
             v-if="$v.form.secondName.$dirty && !$v.form.secondName.required"
             >*Это обязательное поле
             </p>
             <p
             v-if="$v.form.secondName.$dirty && !$v.form.secondName.minLength"
             >*Слишком мало букв
             </p>
        </div>
        <div class="form-group input-form" >
            <span>Имя</span>
            <input type="text" placeholder="Иван" class="input" v-model.trim="form.firstName">
            <p
             v-if="$v.form.firstName.$dirty && !$v.form.firstName.required"
             >*Это обязательное поле
             </p>
             <p
             v-if="$v.form.firstName.$dirty && !$v.form.firstName.minLength"
             >*Слишком мало букв
             </p>
        </div>
        <div class="form-group input-form" >
            <span>Отчество</span>
            <input type="text" placeholder="Иванович" class="input" v-model.trim="form.thirdName">
            <p
             v-if="$v.form.thirdName.$dirty && !$v.form.thirdName.minLength"
             >*Слишком мало букв
             </p>
        </div>
        <div class="form-group date">
            <span>Дата рождения</span>
            <div class="input-numbers">
                <div class="number-fields">
                    <span>День</span>
                    <input type="text" placeholder="01" class="input input-number" v-model.trim="form.day">
                    <p
                    v-if="$v.form.day.$dirty && !$v.form.day.required"
                    > *Это обязательное поле
                    </p>
                    <p
                    v-if="$v.form.day.$dirty && !$v.form.day.minLength"
                    > *Слишком мало цифр
                    </p>
                    <p
                    v-if="$v.form.day.$dirty && !$v.form.day.maxLength"
                    > *Слишком много цифр 
                    </p>
                </div>
                <div class="number-fields">
                    <span>Месяц</span>
                    <input type="text" placeholder="01" class="input input-number" v-model.trim="form.month">
                    <p
                    v-if="$v.form.month.$dirty && !$v.form.month.required"
                    > *Это обязательное поле
                    </p>
                    <p
                    v-if="$v.form.month.$dirty && !$v.form.month.minLength"
                    > *Слишком мало цифр 
                    </p>
                    <p
                    v-if="$v.form.month.$dirty && !$v.form.month.maxLength"
                    > *Слишком много цифр 
                    </p>
                </div>
                <div class="number-fields">
                    <span>Год</span>
                    <input type="text" placeholder="2001" class="input input-number" v-model.trim="form.year">
                    <p
                    v-if="$v.form.year.$dirty && !$v.form.year.required"
                    > *Это обязательное поле
                    </p>
                    <p
                    v-if="$v.form.year.$dirty && !$v.form.year.minLength"
                    > *Слишком мало цифр
                    </p>
                    <p
                    v-if="$v.form.year.$dirty && !$v.form.year.maxLength"
                    > *Слишком много цифр
                    </p>
                </div>
            </div>
            <span></span>
        </div>
        <div class="form-group input-form" >
            <span>Номер телефона</span>
            <div class="number-form input_form">
                <div class="number-field">
                    <span class="plus-seven">+7 </span>
                    <input type="text" placeholder="1234567890" class="input input-phone" v-model.trim="form.number">
                </div>
                <p
                    v-if="$v.form.number.$dirty && !$v.form.number.required"
                    >*Это обязательное поле
                </p>
                <p
                    v-if="$v.form.number.$dirty && !$v.form.number.minLength"
                    >*Слишком мало цифр
                </p>
                <p
                    v-if="$v.form.number.$dirty && !$v.form.number.maxLength"
                    >*Слишком много цифр
                </p>
            </div>
        </div>
        <div class="form-group gender" >
            <span>Пол</span>
            <label class="form-group radio-form" :class="{ active: !activeRadio }">
                <input type="radio" class="input radio" name="genderRadio" id="male" value="male" v-model="form.gender" @change="activeRadioToggle">
                <label for="male">Мужчина</label>
            </label>
            <label class="form-group radio-form" :class="{ active: activeRadio }">
                <input type="radio" class="input radio" name="genderRadio" id="female" value="female" v-model="form.gender" @change="activeRadioToggle">
                <label for="female">Женщина</label>
            </label>
        </div>
        <div class="form-group selectors">
            <span>Группа клиентов </span>
            <select name="" id="" multiple v-model="form.chosenClientGroups" class="select">
                <option
                 v-for="(group, index) in form.clientGroups"
                 :key="index"
                 :value="group.value"
                 >
                 {{ group.label }}
                </option>
            </select>
            <p
             v-if="$v.form.chosenClientGroups.$dirty && !$v.form.chosenClientGroups.required"
             >*Это обязательное поле
             </p>
        </div>
        <div class="form-group selectors">
            <span>Лечащий врач </span>
            <select name="" id="" v-model="form.doctor" class="select">
                <option
                 v-for="(doctor, index) in form.inCharge"
                 :value="doctor.value"
                 :key="index"
                 >
                 {{ doctor.label }}
                </option>
            </select>
        </div>
        <label class="form-group checkbox" :class="{ active: activeCheckbox }">
            <input type="checkbox" class="input check" id="SMS" v-model="form.sendSMS" @click="activeCheckboxToggle" >
            <label for="SMS">Не отправлять СМС</label>
        </label>
        <p class="form-name">Адрес</p>
        <div class="form-group input-form">
            <span>Индекс</span>
            <input type="text" class="input" v-model.trim="form.index">
        </div>
     
        <div class="form-group input-form">
            <span>Страна</span>
            <input type="text" class="input" v-model.trim="form.country">
        </div>
        <div class="form-group input-form">
            <span>Область</span>
            <input type="text" class="input" v-model.trim="form.area">
        </div>
        <div class="form-group input-form">
            <span>Город</span>
            <input type="text" class="input" v-model.trim="form.city">
            <p
             v-if="$v.form.city.$dirty && !$v.form.city.required"
             >*Это обязательное поле
             </p>
        </div>
        <div class="form-group input-form">
            <span>Улица</span>
            <input type="text" class="input" v-model.trim="form.street">
        </div>
        <div class="form-group input-form">
            <span>Дом</span>
            <input type="text" class="input" v-model.trim="form.house">
        </div>
        <p class="form-name">Паспорт</p>
        <div class="form-group input-form">
            <span>Тип документа</span>
            <select type="text" class="input" v-model.trim="form.documentType">
                <option 
                 v-for="(document, index) in form.documentTypes"
                 :key="index"
                 :value="document.value"
                 >
                 {{ document.label }}</option>
            </select>
            <p
             v-if="$v.form.documentType.$dirty && !$v.form.documentType.required"
             >*Это обязательное поле
             </p>
        </div>
        <div class="form-group input-form">
            <span>Серия</span>
            <input type="text" class="input" v-model.trim="form.documentSeries">
        </div>
        <div class="form-group input-form">
            <span>Номер</span>
            <input type="text" class="input" v-model.trim="form.documentNumber">
        </div>
        <div class="form-group input-form">
            <span>Кем выдан</span>
            <input type="text" class="input" v-model.trim="form.issuedBy">
            <p
             v-if="$v.form.firstName.$dirty && !$v.form.firstName.minLength"
             >*Слишком мало букв
             </p>
        </div>
        <div class="form-group date">
            <span>Дата выдачи</span>
            <div class="input-numbers">
                <div class="number-fields">
                    <span>День</span>
                    <input type="text" placeholder="01" class="input-number input" v-model.trim="form.issueDay">
                    <p
                    v-if="$v.form.issueDay.$dirty && !$v.form.issueDay.required"
                    >*Это обязательное поле
                    </p>
                    <p
                    v-if="$v.form.issueDay.$dirty && !$v.form.issueDay.minLength"
                    >*Слишком мало цифр
                    </p>
                    <p
                    v-if="$v.form.issueDay.$dirty && !$v.form.issueDay.maxLength"
                    >*Слишком много цифр
                    </p>
                </div>
                <div class="number-fields">
                    <span>Месяц</span>
                    <input type="text" placeholder="01" class="input-number input" v-model.trim="form.issueMonth">
                    <p
                    v-if="$v.form.issueMonth.$dirty && !$v.form.issueMonth.required"
                    >*Это обязательное поле
                    </p>
                    <p
                    v-if="$v.form.issueMonth.$dirty && !$v.form.issueMonth.minLength"
                    >*Слишком мало цифр
                    </p>
                    <p
                    v-if="$v.form.issueMonth.$dirty && !$v.form.issueMonth.maxLength"
                    >*Слишком много цифр
                    </p>
                </div>
                <div class="number-fields">
                    <span>Год</span>
                    <input type="text" placeholder="2001" class="input-number input" v-model.trim="form.issueYear">
                    <p
                    v-if="$v.form.issueYear.$dirty && !$v.form.issueYear.required"
                    >*Это обязательное поле
                    </p>
                    <p
                    v-if="$v.form.issueYear.$dirty && !$v.form.issueYear.minLength"
                    >*Слишком мало цифр
                    </p>
                    <p
                    v-if="$v.form.issueYear.$dirty && !$v.form.issueYear.maxLength"
                    >*Слишком много цифр
                    </p>
                </div>
             </div>
        </div>
        <button type="submit" class="submit-button">Отправить</button>
      </form>
      <SuccessMessage v-if="formComplete" @back="formCompleteToggle"/>
  </div>
</template>

<script>
import { validationMixin } from 'vuelidate'
import { required, minLength, maxLength } from 'vuelidate/lib/validators'
import SuccessMessage from './SuccessMessage'
import Cover from './Cover'

export default {
    mixins: [validationMixin],
    components: {
        SuccessMessage,
        Cover
    },
    data() {
        return {
            formComplete: false,
            activeRadio: false,
            activeCheckbox: false,
            form: {
                firstName: '',
                secondName: '',
                thirdName: '',
                day: '',
                month: '',
                year: '',
                number: '',
                chosenClientGroups: [],
                clientGroups: [
                {
                    label: 'VIP',
                    value: 'VIP'
                },
                {
                    label: 'Проблемные',
                    value: 'Problematic'
                },
                {
                    label: 'ОМС',
                    value: 'Medical Insurance'
                }
                ],
                doctor: 'Ivanov',
                inCharge: [
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
                    value: 'Chernisheva'
                }
                ],
                gender: 'male',
                sendSMS: false,
                index: '',
                country: '',
                area: '',
                city: '',
                street: '',
                house: '',
                documentType: 'pass',
                documentTypes: [
                    {
                        label: 'Паспорт',
                        value: 'pass'
                    },
                    {
                        label: 'Свидетельство о рождении',
                        value: 'birthCertificate'
                    },
                    {
                        label: 'Вод. удостоверение',
                        value: 'driversLicense'
                    },
                ],
                documentSeries: '',
                documentNumber: '',
                issuedBy: '',
                issueDay: '',
                issueMonth: '',
                issueYear: ''
            },
        }
    },
    validations: {
        form: {
            firstName: { required, minLength: minLength(1) },
            secondName: { required, minLength: minLength(1) },
            thirdName: { minLength: minLength(1) },
            number: { required, minLength: minLength(10), maxLength: maxLength(10) },
            day: { required, minLength: minLength(2), maxLength: maxLength(2) },
            month: { required, minLength: minLength(2), maxLength: maxLength(2) },
            year: { required, minLength: minLength(4), maxLength: maxLength(4) },
            chosenClientGroups:{ required },
            city: { required },
            documentType: { required },
            documentSeries: { minLength: minLength(4), maxLength: maxLength(11) },
            documentNumber: { minLength: minLength(6), maxLength: maxLength(16) },
            issuedBy: { minLength: minLength(1) },
            issueDay: { required, minLength: minLength(2), maxLength: maxLength(2) },
            issueMonth: { required, minLength: minLength(2), maxLength: maxLength(2) },
            issueYear: { required, minLength: minLength(4), maxLength: maxLength(4) },
        }
    },
    methods: {
        formCompleteToggle() {
            return this.formComplete = !this.formComplete
        },
        formCheck() {
            this.$v.form.$touch()
            if (this.$v.form.$error) {
                console.log('succeed')
            } else {
                this.formCompleteToggle()
            }
        },
        activeCheckboxToggle() {
            this.activeCheckbox = !this.activeCheckbox
        },
        activeRadioToggle() {
            this.activeRadio = !this.activeRadio
        },
    }
}
</script>

<style scoped lang="scss">
    .forms-container {
        margin: 1rem auto;
        background: #FFFFFF;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 1.2rem;
        max-width: 95%;
        border-radius: 8px;
    }
    .form {
        background: #FFFFFF;
        display: flex;
        align-items: left;
        flex-direction: column;
        max-width: 80%;
        margin-top: 2rem;
        margin-bottom: 2rem;
        padding: 2rem;
        
    }
    .form-group {
        display: flex;
        margin-bottom: .5rem;
        max-width: 100%;
        justify-content: center;
        span {
            font-weight: bold;
            margin: .8rem 0 .8rem 0;
        }
        p {
            font-size: .9rem;
            color: #CD5C5C;
        }
    }
    .form-name {
        font-size: 2rem;
        font-weight: bold;
    }
    .input-form {
        flex-direction: column;
    }
    .number-form {
        display: flex;
        flex-direction: column;
    }
    .number-field {
        display: flex;
    }
    .plus-seven {
        font-size: 1.5rem;
    }
    .select {
        font-size: 1rem;
        margin: .5rem;
        padding: .2em;
    }
    .checkbox {
        flex-direction: row;
        background: #E8E8E8;
        padding: 2rem 0;
        align-items: center;
        justify-content: left;
    }
    .check {
        margin: 0 1em;
    }
    
    .gender {
        display: flex;
        flex-direction: column;
    }
    .selectors {
        align-items: left;
        justify-content: left;
        flex-direction: column;
    }
    .radio-form {
        align-items: center;
        justify-content: left;
        padding: 2rem 0;
        background: #E8E8E8;
    }
    .radio {
        margin: 0 1rem;
    }
    .active {
        background: #FFFFFF;
        border: 2px solid #0061d9;
    }
    .input {
        padding: .3rem;
    }
    .date {
        display: flex;
        flex-direction: column;
        justify-content: space-around;
    }
    .input-phone {
        max-width: 100%;
    }
    .input-numbers {
        display: flex;
        align-self: start;
        max-width: 100%;
        justify-content: space-between;
    }
    .number-fields {
        max-width: 30%;
    }
    .input-number {
        max-width: 100%;
    }
    .submit-button {
        padding: .8rem;
        background: #0061d9;
        border: none;
        color: #FFFFFF;
        font-size: 1.5rem;
        border-radius: 8px;
        :active {
            border: none;
        }
    }
</style>