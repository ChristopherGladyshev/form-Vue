<template>
  <div id="app">
    <FormNewUser></FormNewUser>
  </div>
</template>

<script>
import FormNewUser from './components/FormNewUser';

export default {
 
  components: {
    'FormNewUser': FormNewUser,
  }
}
</script>

<style>
#app{
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #111;
  color: #fff;
}
</style>
