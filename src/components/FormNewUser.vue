<template>
  <form @submit.prevent="submit">
    <h1>New User</h1>
    <div class="container__input">
      <label for="surname">Фамилия</label>
      <input type="text" placeholder="Фамилия" id="surname" v-model="surname" />
    </div>
    <div class="container__input">
      <label
        for="userName"
        :class="{'error': ($v.userName.$dirty && !$v.userName.required) || ($v.userName.$dirty && !$v.userName.minLength)}"
      >*Имя</label>
      <input
        type="text"
        placeholder="Имя"
        id="userName"
        v-model.trim="$v.userName.$model"
        :class="{'invalid': ($v.userName.$dirty && !$v.userName.required) || ($v.userName.$dirty && !$v.userName.minLength)}"
      />
      <div
        class="errorMessage"
        :class="{'error': ($v.userName.$dirty && !$v.userName.required) || ($v.userName.$dirty && !$v.userName.minLength)}"
      >Поле, обязательное для заполнения не менее {{$v.userName.$params.minLength.min}} символов.</div>
    </div>
    <div class="container__input">
      <label
        for="patronymic"
        :class="{'error': ($v.patronymic.$dirty && !$v.patronymic.required) || ($v.patronymic.$dirty && !$v.patronymic.minLength)}"
      >*Отчество</label>
      <input
        type="text"
        placeholder="Отчество"
        id="patronymic"
        v-model.trim="$v.patronymic.$model"
        :class="{'invalid': ($v.patronymic.$dirty && !$v.patronymic.required) || ($v.patronymic.$dirty && !$v.patronymic.minLength)}"
      />
      <div
        class="errorMessage"
        :class="{'error': ($v.patronymic.$dirty && !$v.patronymic.required) || ($v.patronymic.$dirty && !$v.patronymic.minLength)}"
      >Поле, обязательное для заполнения не менее {{$v.patronymic.$params.minLength.min}} символов.</div>
    </div>
    <div class="container__input">
      <label for="date">Дата рождения</label>
      <input type="text" placeholder="Фамилия" id="date" v-model="date" />
    </div>
    <div class="container__input">
      <label
        for="phone"
        :class="{'error': ($v.phone.$dirty && !$v.phone.validFormat) || ($v.phone.$dirty && !$v.phone.minLength)}"
      >Номер телефона</label>
      <input
        type="tel"
        id="phone"
        name="phone"
        placeholder="+7 (***) ***-**-**"
        v-model.trim="$v.phone.$model"
        :class="{'invalid': ($v.phone.$dirty && !$v.phone.validFormat) || ($v.phone.$dirty && !$v.phone.minLength)}"
      />
      <div
        class="errorMessage"
        :class="{'error': ($v.phone.$dirty && !$v.phone.validFormat) || ($v.phone.$dirty && !$v.phone.minLength)}"
      >Поле, обязательное для заполнения не менее {{$v.phone.$params.minLength.min}} символов.</div>
    </div>
    <div class="container__input">
      <label for="date">Пол</label>
      <input type="text" placeholder="Man/Woman" id="pol" v-model="pol" />
    </div>
    <div class="container__input">
      <label for="RroupsClients">*Группа клиентов</label>
      <select
        id="RroupsClients"
        v-model.trim="$v.RroupsClients.$model"
        multiple
        :class="{'invalid': ($v.RroupsClients.$dirty && !$v.RroupsClients.required)}"
      >
        <option disabled>Выбирите значение</option>
        <option>VIP</option>
        <option>Проблемные</option>
        <option>ОМС</option>
      </select>
      <div
        class="errorMessage"
        :class="{'error': ($v.RroupsClients.$dirty && !$v.RroupsClients.required)}"
      >Поле, обязательное для заполнения.</div>
    </div>
    <div class="container__input">
      <label for="doctor">Лечащий врач</label>
      <select id="doctor" v-model="doctor">
        <option value hidden>Выбирите значение</option>
        <option>Иванов</option>
        <option>Захаров</option>
        <option>Чернышева</option>
      </select>
    </div>
    <div class="container__input">
      <input class="checkbox" type="checkbox" id="sms" v-model="sms" />
      <label for="one">Не отправлять СМС</label>
    </div>
    <h3>Адрес</h3>
    <div class="container__input">
      <label for="index">Индекс</label>
      <input type="text" id="index" name="index" placeholder="Индекс" v-model.trim="index" />
    </div>
    <div class="container__input">
      <label for="country">Страна</label>
      <input type="text" id="country" name="country" placeholder="Страна" v-model.trim="country" />
    </div>
    <div class="container__input">
      <label for="region">Область</label>
      <input type="text" id="region" name="region" placeholder="Область" v-model.trim="region" />
    </div>
    <div class="container__input">
      <label for="city">Город</label>
      <input type="text" id="city" name="city" placeholder="Город" v-model.trim="city" />
    </div>
    <div class="container__input">
      <label
        for="street"
        :class="{'error': ($v.street.$dirty && !$v.street.required) || ($v.street.$dirty && !$v.street.minLength)}"
      >*Улица</label>
      <input
        type="text"
        id="street"
        name="street"
        placeholder="Улица"
        v-model.trim="$v.street.$model"
        :class="{'invalid': ($v.street.$dirty && !$v.street.required) || ($v.street.$dirty && !$v.street.minLength)}"
      />
      <div
        class="errorMessage"
        :class="{'error': ($v.street.$dirty && !$v.street.required) || ($v.street.$dirty && !$v.street.minLength)}"
      >Поле, обязательное для заполнения не менее {{$v.street.$params.minLength.min}} символов.</div>
    </div>
    <div class="container__input">
      <label for="home">Дом</label>
      <input type="text" id="home" name="home" placeholder="Дом" v-model.trim="home" />
    </div>
    <h3>Паспорт</h3>

    <div class="container__input">
      <label for="document">Тип документа</label>
      <select
        id="document"
        v-model.trim="$v.document.$model"
        :class="{'invalid': ($v.document.$dirty && !$v.document.required)}"
      >
        <option value hidden>Выбирите значение</option>
        <option>Паспорт</option>
        <option>Свидетельство о рождении</option>
        <option>Вод удостоверение</option>
      </select>
      <div
        class="errorMessage"
        :class="{'error': ($v.document.$dirty && !$v.document.required)}"
      >Поле, обязательное для заполнения.</div>
    </div>
    <div class="container__input">
      <label for="series">Серия</label>
      <input type="text" id="series" name="series" placeholder="Серия" v-model.trim="city" />
    </div>
    <div class="container__input">
      <label for="city">Номер</label>
      <input type="text" id="city" name="city" placeholder="Город" v-model.trim="city" />
    </div>
    <div v-bind="NewUser" class="NewUser" :v-if="{'ok': NewUser}">
      <p>Пользователь создан</p>
    </div>
    <dir class="container__submit">
      <button type="submit">Create User</button>
    </dir>
  </form>
</template>

<script>
import { required, minLength } from "vuelidate/lib/validators";

export default {
  name: "login",
  data: () => ({
    surname: null,
    userName: null,
    patronymic: null,
    date: null,
    phone: null,
    pol: null,
    RroupsClients: [],
    doctor: null,
    sms: null,
    index: null,
    country: null,
    region: null,
    city: null,
    street: null,
    home: null,
    document: [],
    series: null,
    NewUser: false,
  }),
  validations: {
    surname: {
      required,
      minLength: minLength(6),
    },
    userName: {
      required,
      minLength: minLength(3),
    },
    patronymic: {
      required,
      minLength: minLength(3),
    },
    phone: {
      validFormat: (val) =>
        /^((8|\+7)[\- ]?)?(\(?\d{3}\)?[\- ]?)?[\d\- ]{7,10}$/.test(val),
      minLength: minLength(11),
    },
    RroupsClients: {
      required,
    },
    street: {
      required,
      minLength: minLength(3),
    },
    document: {
      required,
    },
  },
  methods: {
    submit() {
      if (this.$v.$invalid) {
        console.log(this.$v.RroupsClients.$model);
        this.$v.$touch();
        return;
      }
    },
  },
};
</script>


<style>
form {
  width: 300px;
  border: 1px solid white;
  border-radius: 20px;
  padding: 10px 15px 10px 10px;
  background: rgba(255, 255, 255, 0.164);
  text-align: center;
  font-family: Arial, sans-serif;
}
.container__input {
  text-align: start;
  position: relative;
  margin-top: 10px;
}
.errorMessage {
  padding-top: 10px;
  display: none;
  text-align: start;
}
.error {
  color: red;
  display: block;
}

label {
  position: absolute;
  top: 0;
  left: 0;
}
input {
  width: 100%;
  height: 30px;
  border: 1px solid #111;
  border-radius: 5px;
  margin-top: 20px;
}
.checkbox {
  width: 20px;
}
select {
  width: 100%;
  border: 1px solid #111;
  border-radius: 5px;
  margin-top: 20px;
}
input:active {
  border: 1px solid #111;
}
input:focus {
  outline: none;
}
.invalid {
  color: red;
  border: 1px solid red;
  background: rgba(255, 0, 0, 0.404);
  transition: 0.3s;
}

.container__submit {
  width: 100%;
  height: 100%;
  text-align: center;
  padding: 0px;
  margin: 10px 0px 0px 0px;
}
.container__submit button {
  width: 100px;
  height: 40px;
  border: 1px solid blue;
  background: blue;
  color: #fff;
  border-radius: 20px;
  cursor: pointer;
  transition: 0.5s;
}
.container__submit button:hover {
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
}
.NewUser{
  display: none;
}

.ok{
  display: block;
  border: 1px solid white;
}
</style>