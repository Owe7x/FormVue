<template>
  <div>
    <form @submit.prevent="submit">
    <div class="row">
      <div class="col-6">
        <div class="field">
          <div class="form-group" :class="{ 'form-group--error': $v.surname.$error }">
            <label class="form__label">Фамилия</label>
            <input class="form__input" v-model.trim="$v.surname.$model"/>
          </div>
          <div class="error" v-if="!$v.surname.required">Поле обязательно для заполнения</div>
          <div class="error" v-if="!$v.surname.minLength">Фамилия должно иметь как минимум  {{$v.surname.$params.minLength.min}} буквы.</div>
        </div>
      </div>
      <div class="col-6">
        <div class="field">
          <div class="form-group" :class="{ 'form-group--error': $v.name.$error }">
            <label class="form__label">Имя</label>
            <input class="form__input" v-model.trim="$v.name.$model"/>
          </div>
          <div class="error" v-if="!$v.name.required">Поле обязательно для заполнения</div>
          <div class="error" v-if="!$v.name.minLength">Имя должно иметь как минимум  {{$v.name.$params.minLength.min}} буквы.</div>
        </div>
      </div>
      <div class="col-6">
        <div class="field">
          <div class="form-group" :class="{ 'form-group--error': $v.middleName.$error }">
            <label class="form__label">Отчество</label>
            <input class="form__input" v-model.trim="$v.middleName.$model"/>
          </div>
          <div class="error" v-if="!$v.middleName.minLength">Имя должно иметь как минимум  {{$v.middleName.$params.minLength.min}} буквы.</div>
        </div>
      </div>
      <div class="col-6">
        <div class="field">
          <div class="form-group" :class="{ 'form-group--error': $v.birthday.$error }">
            <label class="form__label">Дата рождения</label>
            <input class="form__input" v-model.trim="$v.birthday.$model"/>
          </div>
          <div class="error" v-if="!$v.birthday.required">Поле обязательно для заполнения</div>
          <div class="error" v-if="$v.birthday.$error">Дата выдачи паспорта должна быть в формате ДД.ММ.ГГГГ</div>
        </div>
      </div>
      <div class="col-6">
        <div class="field">
          <div class="form-group" :class="{ 'form-group--error': $v.userNumber.$error }">
            <label class="form__label">Номер телефона</label>
            <input class="form__input" type="tel" v-model="userNumber" maxlength="12">
          </div>
          <div class="error" v-if="!$v.userNumber.required">Поле обязательно для заполнения</div>
          <div class="error" v-if="!$v.userNumber.minLength">Номер телефона должен состоять из 11 цифр</div>
        </div>
      </div>
      <div class="col-6">
        <div class="field">
          <div class="form-group" >
            <label class="form__label">Выберите пол</label>
            <multiselect v-model="gender" :options="optionsGender" :searchable="false" :close-on-select="false" :show-labels="false" placeholder="Выберите значение"></multiselect>
          </div>
        </div>
      </div>
      <div class="col-6">
        <div class="field">
          <div class="form-group">
            <label class="form__label">Группа клиентов</label>
            <multiselect v-model="client" :options="optionsClient" :multiple="true" :close-on-select="false" :clear-on-select="false" :preserve-search="true" placeholder="Выберите значение" label="name" track-by="name" :preselect-first="true">
              <template slot="selection" slot-scope="{ values,  isOpen }"><span class="multiselect__single" v-if="values.length &amp;&amp; !isOpen">{{ values.length }} значения выбраны</span></template>
            </multiselect>
            <div class="error" v-if="!$v.client.required">Поле обязательно для заполнения</div>
          </div>
        </div>
      </div>
      <div class="col-6">
        <div class="field">
          <div class="form-group">
            <label class="form__label">Лечащий врач</label>
            <multiselect v-model="doctor" :options="optionsDoctor" :searchable="false" :close-on-select="false" :show-labels="false" placeholder="Выберите значение"></multiselect>
          </div>
        </div>
      </div>
      <div class="col-12">
        <div class="field">
          <label for="">
            <input type="checkbox"> Не отправлять СМС
          </label>
        </div>
      </div>
      <div class="col-6">
        <div class="field">
          <div class="form-group" :class="{ 'form-group--error': $v.index.$error }">
            <label class="form__label">Индекс</label>
            <input class="form__input" v-model.trim="$v.index.$model"/>
          </div>
        </div>
      </div>
      <div class="col-6">
        <div class="field">
          <div class="form-group" :class="{ 'form-group--error': $v.country.$error }">
            <label class="form__label">Страна</label>
            <input class="form__input" v-model.trim="$v.country.$model"/>
          </div>
        </div>
      </div>
      <div class="col-6">
        <div class="field">
          <div class="form-group" :class="{ 'form-group--error': $v.area.$error }">
            <label class="form__label">Область</label>
            <input class="form__input" v-model.trim="$v.area.$model"/>
          </div>
        </div>
      </div>
      <div class="col-6">
        <div class="field">
          <div class="form-group" :class="{ 'form-group--error': $v.city.$error }">
            <label class="form__label">Город</label>
            <input class="form__input" v-model.trim="$v.city.$model"/>
          </div>
          <div class="error" v-if="!$v.city.required">Поле обязательно для заполнения</div>
        </div>
      </div>
      <div class="col-6">
        <div class="field">
          <div class="form-group" :class="{ 'form-group--error': $v.street.$error }">
            <label class="form__label">Улица</label>
            <input class="form__input" v-model.trim="$v.street.$model"/>
          </div>
        </div>
      </div>
      <div class="col-6">
        <div class="field">
          <div class="form-group" :class="{ 'form-group--error': $v.house.$error }">
            <label class="form__label">Дом</label>
            <input class="form__input" v-model.trim="$v.house.$model"/>
          </div>
        </div>
      </div>
      <div class="col-6">
        <div class="field">
          <div class="form-group">
            <label class="form__label">Тип документа:</label>
            <multiselect v-model="document" :options="optionsDocument" :multiple="true" :close-on-select="false" :clear-on-select="false" :preserve-search="true" placeholder="Выберите значение" label="name" track-by="name" :preselect-first="true">
              <template slot="selection" slot-scope="{ values,  isOpen }"><span class="multiselect__single" v-if="values.length &amp;&amp; !isOpen">{{ values.length }} значения выбраны</span></template>
            </multiselect>
            <div class="error" v-if="!$v.document.required">Поле обязательно для заполнения</div>
          </div>
        </div>
      </div>
    <div class="col-6">
      <div class="field">
        <div class="form-group" :class="{ 'form-group--error': $v.passportData.$error }">
          <label class="form__label">Серия и номер паспорта</label>
          <input class="form__input" id="passport_data" type="text" v-model="passportData">
          <div class="error" v-if="$v.passportData.$error">
            Серия и номер паспорта должны быть в формате 1234 567890
          </div>
        </div>
      </div>
    </div>
    <div class="col-6">
      <div class="field">
        <div class="form-group" :class="{ 'form-group--error': $v.extradition.$error }">
          <label class="form__label">Кем выдан</label>
          <input class="form__input" v-model.trim="$v.extradition.$model">
        </div>
      </div>
    </div>
    <div class="col-6">
      <div class="field">
        <div class="form-group" :class="{ 'form-group--error': $v.extradition.$error }">
          <label class="form__label">Дата выдачи паспорта</label>
          <input class="form__input" v-model="passportDate" @blur="$v.passportDate.$touch()" >
          <div class="error" v-if="$v.passportDate.$error">
            Дата выдачи паспорта должна быть в формате ДД.ММ.ГГГГ
          </div>
        </div>
      </div>
    </div>
    </div>
    <button class="button" type="submit" :disabled="submitStatus === 'PENDING'">Отправить!</button>
    <p class="typo__p" v-if="submitStatus === 'OK'">Спасибо за отправку!</p>
    <p class="typo__p_error" v-if="submitStatus === 'ERROR'">Пожалуйста, заполните форму правильно.</p>
    <p class="typo__p" v-if="submitStatus === 'PENDING'">Отправка...</p>
  </form>

  </div>
  
</template>

<script>
import Multiselect from 'vue-multiselect'
import { required, maxLength, sameAs, minLength } from "vuelidate/lib/validators";
import moment from "moment";


export default {
  data() {
    return {
      name: '',
      surname: '',
      middleName: '',
      birthday: null,
      userNumber: '+7',
      gender: '',
      optionsGender: ['Мужской', 'Женский'],
      client: '',
      optionsClient: [
        {name: 'VIP'},
        {name: 'Проблемные'},
        {name: 'ОМС'}
      ],
      doctor: '',
      optionsDoctor: ['Иванов', 'Захаров', 'Чернышева'],
      index: '',
      country: '',
      area: '',
      city: '',
      street: '',
      house: '',
      document: '',
      optionsDocument: [
        {name: 'Паспорт'},
        {name: 'Свидетельство о рождении'},
        {name: 'Вод.удостоверение'}
      ],
      passportData: null,
      passportDate: null,
      extradition: '',
      submitStatus: null
    };
  },
  components: {
    Multiselect,
  },

  validations: {
    name: {
      required,
      minLength: minLength(2)
    },
    surname: {
      required,
      minLength: minLength(2)
    },
    middleName: {
      minLength: minLength(2)
    },
    birthday: {
      required,
      validDate: val => moment(val, "DD.MM.YYYY", true).isValid(),
    },
    userNumber: { 
      required,
      maxLength: maxLength(12),
      minLength: minLength(12)
    },
    client: {
      required
    },
    index: {

    },
    country: {

    },
    area: {

    },
    city: {
      required
    },
    street: {

    },
    house: {
      
    },
    document: {
      required
    },
    passportData: {
      required,
      validFormat: val => /^\d{4} \d{6}$/.test(val),
    },
    extradition: {

    },
    passportDate: {
      required,
      validDate: val => moment(val, "DD.MM.YYYY", true).isValid(),
    },
  },
  watch: {
    userNumber: function(newNumber) {
      if (newNumber.length < 2) {
        this.userNumber = '+7';
      }
    }
  },
  methods: {
    submit() {
      console.log('submit!')
      this.$v.$touch()
      if (this.$v.$invalid) {
        this.submitStatus = 'ERROR'
      } else {
        // do your submit logic here
        this.submitStatus = 'PENDING'
        setTimeout(() => {
          this.submitStatus = 'OK'
        }, 500)
      }
    }
  },
};
</script>
<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>
<style lang="sass" >

form 
  width: 600px
  padding: 32px
  border-radius: 10px
  box-shadow: 0 4px 16px #ccc
  font-family: sans-serif
  letter-spacing: 1p
  margin: 50px auto 0px
.button
  width: 200px
  height: 35px
  background: #ffffff
  border: 1px solid #9e9e9e
  border-radius: 5px
  color: #9e9e9e
  &:hover
    background: #9e9e9e
    color: #ffffff
  &:focus
    outline: none
    background: #9e9e9e
    color: #ffffff
.typo__p
  color: #9e9e9e
.typo__p_error
  color: red
.field 
  max-width: 275px
  margin-bottom: 24px
  .form-group
    position: relative
    margin-top: 20px
    margin-bottom: 20px
    display: flex
    flex-direction: column
    .form__input
      width: 100%
      padding: 0 0 0 0
      border: none
      border-bottom: 1px solid #e0e0e0
      background-color: transparent
      outline: none
      transition: 0.3s
      &:hover
        border-bottom: 1px solid #1a73a8
    .form__input:focus .form__label
      top: -18px
      font-size: 12px
      color: #e0e0e0
    .form__label
      position: absolute
      top: -20px
      z-index: -1
      color: #9e9e9e
      transition: 0.3s
      
.error 
  color: red

</style>