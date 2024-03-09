<template>
  <div class="body-main">
  
    <div class="speaker-form-header"
      v-if="true">
  
      <p v-if="errors.length">
          <b>Пожалуйста верно заполните указанные ошибки:</b>
          <ul>
            <li v-for="(error, index) in errors" :key="index">{{ error }}</li>
          </ul>
      </p>
  
      <div v-if="!errors.length && !isAbleToSend" style="text-align: left;">
         <h1>Регистрация пользователя</h1>
      </div>
  
      <div v-if="isAbleToSend && !errors.length" style="text-align: left;">
         <h1 style='color: green;'>Регистрация прошла успешно!!!</h1>
      </div>
  
        <!-- <pre>
          {{ $v.regForm.clientgroup }}
        </pre> -->
    </div>
      
      
      <form
        id="app"
        @submit="checkForm"
        action="https://vuejs.org/"
        method="post"
        novalidate
        style="display: flex; flex-wrap: wrap; justify-content: space-evenly;">
  
        <div class="speaker-form">
            <div class="">
          
              <div style="width: 100%;">
                <h4 style="">Персональные данные пользователя:</h4>
              </div>
  
                <div class="grid-form-persInfo">
                  <div class="form-row">
                    <div class="">
                      <label class="label form_text red_star" for="lastName">Фамилия</label>
                        <input
                          placeholder="Ваша Фамилия"
                          id="lastName"
                          type="text"
                          lastName="lastName"
                          v-model="regForm.lastName"
                          @blur="$v.regForm.lastName.$touch()"
                          :class="{'is-Invalid': $v.regForm.lastName.$error || showErorr, 'red-empty': !$v.regForm.lastName.alpha, 'Valid': !$v.regForm.lastName.$invalid}"
                        >
                          <div v-if="!$v.regForm.lastName.required && $v.regForm.lastName.$error && $v.regForm.lastName.alpha"
                          class="invalid-data">
                          Поле обязательно к заполнению
                          </div>
                    </div>
                  </div>
                  
                  <div class="form-row">
                    <label class="label form_text red_star" for="firstName">Имя</label>
                      <input
                        placeholder="Ваше Имя"
                        id="firstName"
                        type="text"
                        firstName="firstName"
                        v-model="regForm.firstName"
                        @blur="$v.regForm.firstName.$touch()"
                        :class="{'is-Invalid': $v.regForm.firstName.$error || showErorr, 'red-empty': !$v.regForm.firstName.alpha, 'Valid': !$v.regForm.firstName.$invalid}"
                      >
                        <div v-if="!$v.regForm.firstName.required && $v.regForm.firstName.$error && $v.regForm.firstName.alpha"
                          class="invalid-data">
                          Поле обязательно к заполнению
                        </div>
                  </div>
  
                  <div class="form-row">
                    <label class="label form_text" for="fatherName">Отчество</label>
                      <input
                        placeholder="Ваше Отчетство"
                        id="fatherName"
                        v-model="fatherName"
                        type="text"
                        fatherName="fatherName"
                      >
                  </div>
  
                  <div class="form-row">
                    <label class="label form_text red_star" for="dateBirth">Дата рождения</label>
                      <input
                        class="form-date"
                        id="dateBirth"
                        type="date"
                        v-model="regForm.dateBirth"
                        @blur="$v.regForm.dateBirth.$touch()"
                        :class="{'is-Invalid': $v.regForm.dateBirth.$error || showErorr, 'Valid': !$v.regForm.dateBirth.$invalid}"
                        required>
  
                          <div v-if="!$v.regForm.dateBirth.required && $v.regForm.dateBirth.$error"
                          class="invalid-data">
                          Поле обязательно к заполнению
                          </div>
                  </div>
  
                  <div class="form-row">
                    <label class="label form_text red_star" for="telephone">Номер телефона</label>
                      <input
                      class="form-date"
                      placeholder="79165450221"
                        id="telephone"
                        type="tel"
                        telephone="telephone"
                        maxlength="11"
                        v-model="regForm.telephone"
                        @blur="$v.regForm.telephone.$touch()"
                        :class="{'is-Invalid': $v.regForm.telephone.$error || showErorr, 'red-empty': !$v.regForm.telephone.numeric, 'Valid': !$v.regForm.telephone.$invalid && this.$v.regForm.telephone.$model.charAt(0) === '7'}"
                      required>
  
                        <div v-if="!$v.regForm.telephone.required && $v.regForm.telephone.$error && $v.regForm.telephone.numeric"
                          class="invalid-data">
                          Поле обязательно к заполнению
                        </div>
  
                  </div>
                    <!-- <div v-if="!$v.regForm.firstName.required && $v.regForm.firstName.$error && $v.regForm.firstName.alpha"
                      class="invalid-data">
                      Поле обязательно к заполнению
                    </div> -->
  
                  <div class="form-row">
                    <label class="label form_text" for="sexOrMF">Выберите пол</label>
                      <select
                        class="form-date"
                        id="sexOrMF"
                        v-model="sexOrMF"
                        sexOrMF="sexOrMF"
                      >
                        <option>Мужской</option>
                        <option>Женский</option>
                    </select>
                  </div>
  
                  <div class="form-row">
                    <div class="">
                      <label for="email"
                      class="label form_text red_star">Email</label>
                        <input
                          placeholder="your.email@please.ru"
                          id="email"
                          type="email"
                          email="email"
                          v-model="regForm.email"
                          @blur="$v.regForm.email.$touch()"
                          :class="{'is-Invalid': $v.regForm.email.$error || showErorr, 'Valid': !$v.regForm.email.$invalid}"
                        >
                    </div>
                          <div v-if="!$v.regForm.email.required && $v.regForm.email.$error" class="invalid-data">
                            Поле обязательно к заполнению
                          </div>
  
                          <div v-if="!$v.regForm.email.email" class="invalid-data">
                            email не валиден
                          </div>
                  </div>
  
                  <div class="form_row padding-fix">
                    <span class="form_text label red_star">Категория клиента</span>
                      <div class="multiselect_block"
                        @blur="$v.regForm.clientgroup.$touch()"
                        :class="{'is-Invalid': $v.regForm.clientgroup.$error || showErorr, 'Valid': !$v.regForm.clientgroup.$invalid}">
                        <label for="clientgroup" class="field_multiselect">Категория</label
                          >
                            <input id="checkbox-1" class="multiselect_checkbox" type="checkbox"
                            >
                              <label for="checkbox-1" class="multiselect_label"></label>
                                <select id="clientgroup" class="field_select" name="clientgroup"
                                  v-model="regForm.clientgroup"
                                  required  
                                  multiple>
                                  <option value="VIP">VIP</option>
                                  <option value="Проблемные">Проблемные</option>
                                  <option value="ОМС">ОМС</option>
                                </select>
                          <span class="field_multiselect_help" style="font-size: small;">Вы можете выбрать несколько, если нажать<b>Ctrl(or Command)+Element</b></span>
                      </div>
                    <span class="error_text"></span>
                  </div>
  
                  <div class="form-row">
                      <label class="label form_text" for="movie">Лечащий врач</label>
                        <select
                          class="form-date"
                          placeholder="Выберите лечащего врача"
                          id="movie"
                          v-model="movie"
                          movie="movie"
                        >
                            <option>Иванов</option>
                            <option>Захарова</option>
                            <option>Чернышева</option>
                        </select>
                  </div>
  
                  <div class="form-row" style="padding-top: 30px;">
                    <input id="highload0" class="checkbox-custom"
                    style="height: 13px;"  name="highload0" type="checkbox"
                    >
                      <label for="highload0" style="padding-left: 7px;" class="checkbox-custom-label">
                        <span>Не отправлять смс.</span>
                      </label>
                  </div>
  
                </div>
            </div>
        </div>
  
        <div class="speaker-form">
          <div class="">
  
            <div style="width: 100%;">
              <h4 style="">Адрес:</h4>
            </div>
          
            <div class="grid-form-adres">
              <div class="form-row">
                <div class="">
                  <label for="index" class="label form_text">Индекс</label>
                    <input
                      placeholder="Индекс"
                      id="index"
                      type="text"
                      index="index"
                      v-model="index"
                    >
                </div>
              </div>
                
              <div class="form-row">
                <label class="label form_text" for="country">Страна</label>
                  <input
                    placeholder="Страна"
                    id="country"
                    v-model="country"
                    type="text"
                    country="country"
                  >
              </div>
  
              <div class="form-row">
                <label class="label form_text" for="region">Область</label>
                  <input
                    placeholder="Область"
                    id="region"
                    v-model="region"
                    type="text"
                    region="region"
                  >
              </div>
  
              <div class="form-row">
                <label class="label form_text red_star" for="city">Город</label>
                  <input
                    placeholder="Город"
                    id="city"
                    type="text"
                    city="city"
                    v-model="regForm.city"
                      @blur="$v.regForm.city.$touch()"
                      :class="{'is-Invalid': $v.regForm.city.$error || showErorr, 'Valid': !$v.regForm.city.$invalid}"
                    >
            
                    <div v-if="!$v.regForm.city.required && $v.regForm.city.$error" class="invalid-data">
                      Поле обязательно к заполнению
                    </div>
  
              </div>
  
              <div class="form-row">
                <label class="label form_text" for="telephone">Улица</label>
                  <input
                    placeholder="Улица"
                    id="fatherName"
                    v-model="fatherName"
                    type="text"
                    fatherName="fatherName"
                  >
              </div>
  
              <div class="form-row">
                <label class="label form_text" for="sexOrMF">Дом</label>
                  <input
                    placeholder="Дом"
                    id="fatherName"
                    v-model="fatherName"
                    type="text"
                    fatherName="fatherName"
                  >
              </div>
  
            </div>
  
          </div>
        </div>
  
        <div class="speaker-form">
          <div class="">
  
            <div style="width: 100%;">
              <h4 style="">Удостоверение личности:</h4>
            </div>
  
  
          <div class="grid-form-docType">
            <div class="form-row">
  
              <div class="">
                <label class="label form_text red_star" for="docType">Тип документа</label>
                  <select
                    class="form-date"
                    id="docType"
                    type="text"
                    docType="docType"
                    v-model="regForm.docType"
                    @blur="$v.regForm.docType.$touch()"
                    :class="{'is-Invalid': $v.regForm.docType.$error || showErorr, 'Valid': !$v.regForm.docType.$invalid}"
                    required>
                      <option>Паспорт</option>
                      <option>Свидетельство о рождении</option>
                      <option>Вод удостоверение</option>
                  </select>
  
                  <div v-if="!$v.regForm.docType.required && $v.regForm.docType.$error" class="invalid-data">
                    Поле обязательно к заполнению
                  </div>
              </div>
  
            </div>
  
            <div class="form-row">
  
              <div class="">
                <label class="label form_text" for="docSer">Серия</label>
                  <input
                    placeholder="Серия"
                    id="docSer"
                    type="text"
                    docSer="docSer"
                    v-model="docSer"
                  >
              </div>
  
            </div>
              
            <div class="form-row">
              <label class="label form_text" for="docNum">Номер</label>
                <input
                  placeholder="Номер"
                  id="docNum"
                  v-model="docNum"
                  type="text"
                  docNum="docNum"
                >
            </div>
  
            <div class="form-row">
              <label class="label form_text" for="telephone">Кем выдан</label>
                <input
                  placeholder="Кем выдан"
                  id="docBy"
                  v-model="docBy"
                  type="text"
                  docBy="docBy"
                >
            </div>
  
            <div class="form-row">
              <label class="label form_text red_star" for="docDate">Дата выдачи</label>
                <input
                  class="form-date"
                  placeholder="Дата выдачи"
                  id="docDate"
                  type="date"
                  docDate="docDate"
                    v-model="regForm.docDate"
                    @blur="$v.regForm.docDate.$touch()"
                    :class="{'is-Invalid': $v.regForm.docDate.$error || showErorr, 'red-empty': !$v.regForm.docDate, 'Valid': !$v.regForm.docDate.$invalid}"
                  required>
            </div>
          </div>
          <!-- <button @submit="checkForm()" type="submit" class="btn btn-primary"
          :disabled="false">Следующий шаг
          </button> -->
          </div>
        </div>
        
        <div class="form-row" style="width: 80%;">
          <button @submit="checkForm() && scrollToTop()" type="submit" class="btn btn-primary" style="width: 100%;"
              :disabled="false">Следующий шаг
          </button>
        </div>
      </form>
  
  </div>
  </template>
  
  <script>
  import { required, helpers, minLength, maxLength, numeric, email } from 'vuelidate/lib/validators';
  const alpha = helpers.regex('alpha', /^[a-zA-Za-яёА-ЯЁ]*$/)
  
  export default {
    mounted() {
      const multiselectBlocks = document.querySelectorAll(".multiselect_block");
      multiselectBlocks.forEach(parent => {
        const label = parent.querySelector(".field_multiselect");
        const select = parent.querySelector(".field_select");
        const text = label.innerHTML;
  
        select.addEventListener("change", function() {
          const selectedOptions = Array.from(this.selectedOptions);
  
          label.innerHTML = "";
          for (const option of selectedOptions) {
            const button = document.createElement("button");
            button.type = "button";
            button.className = "btn_multiselect";
            button.textContent = option.value;
            button.onclick = () => {
              option.selected = false;
              button.remove();
              if (!select.selectedOptions.length) label.innerHTML = text;
            };
            label.append(button);
          }
        });
      });
    },
    data() {
      return {
        isAbleToSend: false,
        element: null,
        errors: [],
        regForm: {
          lastName: '',
          firstName: '',
          fatherName: '',
          sexOrMF: '',
          dateBirth: '',
          telephone: '',
          email: '',
          city: '',
          docType: '',
          clientgroup: []
  
        },
        showErorr: false
      };
    },
    // computed: {
    //   isAbleToSend () {
    //     return this.$v.regForm.lastName.$invalid ||
    //             this.$v.regForm.telephone.$invalid ||
    //              this.$v.regForm.email.$invalid
    //   }
    // },
    methods: {
      checkForm: function (e) {
        this.errors = [];
  
        if (this.$v.regForm.lastName.$invalid) {
          this.errors.push('Укажите фамилию.');
          this.showErorr = true;
        } 
  
        if (this.$v.regForm.firstName.$invalid) {
          this.errors.push('Укажите имя.');
          this.showErorr = true;
        }
  
        if (this.$v.regForm.dateBirth.$invalid) {
          this.errors.push('Укажите дату рождения.');
          this.showErorr = true;
          console.log(this.$v.regForm.dateBirth.$model)
        } 
        
        if (this.$v.regForm.telephone.$invalid) {
          this.errors.push('Укажите номер телефона');
          this.showErorr = true;
        }
  
        if (this.$v.regForm.telephone.$model.charAt(0) !== '7' && this.$v.regForm.telephone.$model !== '') {
            this.errors.push('Номер должен начинаться с 7');
            this.showErorr = true;
        }
  
        if (this.$v.regForm.clientgroup.$invalid) {
          this.errors.push('Укажите группу клиентов');
          this.showErorr = true;
        } 
        if (this.$v.regForm.email.$invalid) {
          this.errors.push('Укажите электронную почту.');
          this.showErorr = true;
        } 
        if (this.$v.regForm.city.$invalid) {
          this.errors.push('Укажите город.');
          this.showErorr = true;
        } 
        if (this.$v.regForm.docType.$invalid) {
          this.errors.push('Укажите тип документа.');
          this.showErorr = true;
        } 
  
        if (this.$v.regForm.docDate.$invalid) {
          this.errors.push('Укажите дату выдачи.');
          this.showErorr = true;
        } 
  
        if (!this.errors.length) {
            this.isAbleToSend = true;
        }
  
        window.scrollTo({
          top: 0,
          behavior: 'smooth' // Плавная прокрутка
        });
  
        e.preventDefault();
      },
      validEmail: function (email) {
        var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
        return re.test(email);
      },
    },
    validations: {
      regForm: {
        lastName: {
          required,
          alpha
      },
      firstName: {
          required,
          alpha
      },        
      dateBirth: {
          required
        },
      telephone: {
        required,
        numeric,
        minLength: minLength(11),
        maxLength:  maxLength(11)
      },
      email: {
        required,
        email
      }, 
      clientgroup: {
        required
      },
      city: {
        required,
        alpha,
        minLength: minLength(3),
      },
      docType: {
        required
      },
      docDate: {
        required
      }
    }
    },
    
  }
  
  </script >
  
  <style lang="scss">
  @import '/src/assets/styles/styles';
  
  .is-Invalid {
    background-color: rgb(200, 141, 141) !important;
  }
  
  input {
    height: 28px;
  }
  
  .Valid {
    border-color: green !important;
    background-color: rgb(184, 241, 184) !important
  }
  
  .red-empty {
    background-color: #de3545 !important;
  }
  
  h4 {
    text-align: left;
    margin: 20px 0px;
  }
  
  .label {
    display: block; 
    text-align: left; 
    padding-left: 8px;
    font-size: small;
  }
  
  .grid-form-adres, .grid-form-docType {
    display: grid;
    grid-template-columns: repeat(6, 1fr);  /* Создание колонок, которые автоматически адаптируются к ширине экрана */
    gap: 25px; /* Промежуток между ячейками */
  }
  
  .grid-form-persInfo {
    display: grid;
    grid-template-columns: repeat(5, 1fr);  /* Создание колонок, которые автоматически адаптируются к ширине экрана */
    gap: 25px; /* Промежуток между ячейками */
  }
  
  @media screen and (max-width: 1280px) {
    h1 {
      font-size: x-large;
      white-space: nowrap;
    }
  
    .grid-form-adres, .grid-form-docType, 
    .grid-form-persInfo {
      grid-template-columns: repeat(4, 1fr);
    }
  }
  
  @media screen and (max-width: 1024px) {
    .grid-form-adres, .grid-form-docType, 
    .grid-form-persInfo {
      grid-template-columns: repeat(3, 1fr);
      gap: 0px 30px;
    }
  }
  
  @media screen and (max-width: 779px) {
    .grid-form-adres, .grid-form-docType, 
    .grid-form-persInfo {
      grid-template-columns: repeat(2, 1fr);
      gap: 0px 30px;
    }
  }
  
  @media screen and (max-width: 524px) {
    h1 {
      font-size: 18px;
    }
  
    .speaker-form-header {
      padding: 20px;
    }
    
    .grid-form-adres, .grid-form-docType, 
    .grid-form-persInfo {
      grid-template-columns: repeat(1, 1fr);
      gap: 0px 30px;
    }
  
    .padding-fix {
    padding-bottom: 30px;
    }
  }
  
  /* Мултиселект */
  
  .form_label {
    position: relative;
    min-height: 88px;
  }
  
  .form_text {
    vertical-align: top;
    display: block;
    margin-bottom: 6px;
    font-weight: 500;
    font-size: 12px;
    line-height: 16px;
    letter-spacing: 0.04em;
    color: #686ea1;
  }
  
  .red_star:after {
    content: "*";
    position: relative;
    top: 0;
    font-size: 13px;
    color: #f00;
  }
  
  .form_label input,
  .field_multiselect {
    position: relative;
    width: 100%;
    display: block;
    /* min-height: 46px; */
    border: 1px solid #cdd6f3;
    box-sizing: border-box;
    border-radius: 8px;
    padding: 3px 40px 10px 16px;
    font-size: 14px;
    color: #a8acc9;
    outline-color: #cdd6f3;
  }
  .form_label input::placeholder,
  .field_multiselect::placeholder {
    color: #a8acc9;
  }
  .form_label input:hover,
  .field_multiselect:hover {
    box-shadow: 0 0 2px rgba(0, 0, 0, 0.16);
  }
  .form_label input:focus,
  .field_multiselect:focus {
    box-shadow: 0 0 2px rgba(0, 0, 0, 0.16);
  }
  
  .field_multiselect_help {
    position: absolute;
    max-width: 100%;
    background-color: #fff;
    top: -48px;
    left: 0;
    opacity: 0;
  }
  
  .form_label input.error {
    border-color: #eb5757;
  }
  
  .error_text {
    color: #eb5757;
  }
  
  .field_multiselect {
    display: flex;
    flex-wrap: wrap;
    padding-right: 60px;
  }
  
  .field_multiselect:after {
    content: "";
    position: absolute;
    right: 14px;
    top: 8px;
    width: 6px;
    height: 16px;
    background: url("data:image/svg+xml,%3Csvg width='6' height='16' viewBox='0 0 6 16' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M3 0L6 5H0L3 0Z' fill='%23A8ACC9'/%3E%3Cpath d='M3 16L6 11H0L3 16Z' fill='%23A8ACC9'/%3E%3C/svg%3E") 50% 50% no-repeat;
  }
  
  .multiselect_block {
    position: relative;
    width: 100%;
  }
  
  .field_select {
    position: absolute;
    top: calc(100% - 2px);
    left: 0;
    width: 100%;
    border: 2px solid #cdd6f3;
    border-bottom-right-radius: 2px;
    border-bottom-left-radius: 2px;
    box-sizing: border-box;
    outline-color: #cdd6f3;
    z-index: 6;
  }
  
  .field_select[multiple] {
    overflow-y: auto;
  }
  
  .field_select option {
    display: block;
    padding: 8px 16px;
    width: calc(370px - 32px);
    cursor: pointer;
  }
  .field_select option:checked {
    background-color: #eceff3;
  }
  .field_select option:hover {
    background-color: #d5e8fb;
  }
  
  .field_multiselect button {
    position: relative;
    padding: 5px 30px 4px 4px;
    background: #ebe4fb;
    border-radius: 4px;
    margin-right: 9px;
    margin-bottom: 10px;
  }
  .field_multiselect button:hover, .field_multiselect button:focus {
    background-color: #dbd1ee;
  }
  .field_multiselect button:after {
    content: "";
    position: absolute;
    top: 7px;
    right: 10px;
    width: 16px;
    height: 16px;
    background: url("data:image/svg+xml,%3Csvg width='24' height='24' viewBox='0 0 24 24' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath fill-rule='evenodd' clip-rule='evenodd' d='M19.4958 6.49499C19.7691 6.22162 19.7691 5.7784 19.4958 5.50504C19.2224 5.23167 18.7792 5.23167 18.5058 5.50504L12.5008 11.5101L6.49576 5.50504C6.22239 5.23167 5.77917 5.23167 5.50581 5.50504C5.23244 5.7784 5.23244 6.22162 5.50581 6.49499L11.5108 12.5L5.50581 18.505C5.23244 18.7784 5.23244 19.2216 5.50581 19.495C5.77917 19.7684 6.22239 19.7684 6.49576 19.495L12.5008 13.49L18.5058 19.495C18.7792 19.7684 19.2224 19.7684 19.4958 19.495C19.7691 19.2216 19.7691 18.7784 19.4958 18.505L13.4907 12.5L19.4958 6.49499Z' fill='%234F5588'/%3E%3C/svg%3E") 50% 50% no-repeat;
    background-size: contain;
  }
  
  .multiselect_label {
    position: absolute;
    top: 1px;
    left: 2px;
    width: 100%;
    height: 44px;
    cursor: pointer;
    z-index: 3;
  }
  
  .field_select {
    display: none;
  }
  
  input.multiselect_checkbox {
    position: absolute;
    right: 0;
    top: 0;
    width: 40px;
    height: 40px;
    border: none;
    opacity: 0;
  }
  
  .multiselect_checkbox:checked ~ .field_select {
    display: block;
  }
  
  .multiselect_checkbox:checked ~ .multiselect_label {
    width: 20px;
    left: initial;
    right: 3px;
    background: #ffffff url("data:image/svg+xml,%3Csvg width='24' height='24' viewBox='0 0 24 24' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath fill-rule='evenodd' clip-rule='evenodd' d='M19.4958 6.49499C19.7691 6.22162 19.7691 5.7784 19.4958 5.50504C19.2224 5.23167 18.7792 5.23167 18.5058 5.50504L12.5008 11.5101L6.49576 5.50504C6.22239 5.23167 5.77917 5.23167 5.50581 5.50504C5.23244 5.7784 5.23244 6.22162 5.50581 6.49499L11.5108 12.5L5.50581 18.505C5.23244 18.7784 5.23244 19.2216 5.50581 19.495C5.77917 19.7684 6.22239 19.7684 6.49576 19.495L12.5008 13.49L18.5058 19.495C18.7792 19.7684 19.2224 19.7684 19.4958 19.495C19.7691 19.2216 19.7691 18.7784 19.4958 18.505L13.4907 12.5L19.4958 6.49499Z' fill='%234F5588'/%3E%3C/svg%3E") 50% 50% no-repeat;
  }
  
  .multiselect_checkbox:checked ~ .field_multiselect_help {
    opacity: 1;
  }
  
  
  </style>