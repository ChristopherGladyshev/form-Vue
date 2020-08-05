<template>
  <form @submit.prevent="submit">
    <div>
      <label for="surname">surname</label>
      <input
        type="text"
        placeholder="surname"
        id="surname"
        v-model.trim="surname"
        :class="{'invalid': ($v.surname.$dirty && !$v.surname.required) || ($v.surname.$dirty && !$v.surname.minLength)}"
      />
    </div>
    <button type="submit">create User</button>
  </form>
</template>

<script>
import { required, minLength } from "vuelidate/lib/validators";

export default {
  name: "login",
  data: () => ({
    surname: "",
    userName: "",
  }),
  validations: {
    surname: {
      required,
      minLength: minLength(6),
    },
    userName: { required },
  },
  methods: {
    submit() {
      if (this.$v.$invalid) {
        console.log(this.$v.$invalid);
        this.$v.$touch();
        return;
      }
    },
  },
};
</script>


<style>
form {
  border: 1px solid white;
  padding: 10px;
  background: rgba(255, 255, 255, 0.164);
}
input{
  width: 300px;
  height: 30px;
  border: 1px solid #111;
  border-radius: 5px;
  margin: 20px;
}
input:active{
   border: 1px solid #111;
}
input:focus{
   outline: none;
}
.invalid{
  color: red;
  border: 1px solid red;
  transition: 0.3s;
}
</style>