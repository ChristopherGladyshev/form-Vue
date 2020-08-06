<template>
  <form @submit.prevent="submit">
    <h1>New User</h1>
    <div class="container__input">
      <label for="surname">Фамилия</label>
      <input type="text" placeholder="Фамилия" id="surname" />
    </div>
    <div
      class="errorMessage"
      :class="{'error': ($v.surname.$dirty && !$v.surname.required) || ($v.surname.$dirty && !$v.surname.minLength)}"
    >Фамилия должна иметь не менее {{$v.surname.$params.minLength.min}} символов.</div>
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
      <input type="text" placeholder="Фамилия" id="date" />
    </div>
    <div class="container__input">
      <label
        for="patronymic"
        :class="{'error': ($v.patronymic.$dirty && !$v.patronymic.required) || ($v.patronymic.$dirty && !$v.patronymic.minLength)}"
      >Отчество</label>
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
      <input type="text" placeholder="Man/Woman" id="pol" />
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
        <option>A</option>
        <option>B</option>
        <option>C</option>
      </select>
      <div
        class="errorMessage"
        :class="{'error': ($v.RroupsClients.$dirty && !$v.RroupsClients.required)}"
      >Поле, обязательное для заполнения.</div>
    </div>
    <div class="container__input">
      <label for="doctor">Лечащий врач</label>
      <select
        id="doctor"
        v-model.trim="$v.RroupsClients.$model"
      >
        <option disabled>Выбирите значение</option>
        <option>Иванов</option>
        <option>Захаров</option>
        <option>Чернышева</option>
      </select>
      <div
        class="errorMessage"
        :class="{'error': ($v.RroupsClients.$dirty && !$v.RroupsClients.required)}"
      >Поле, обязательное для заполнения.</div>
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
    phone: null,
    RroupsClients: null,
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
      minLength: minLength(3),
    },
    RroupsClients: {
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
</style>