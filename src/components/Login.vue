<template>
  <div>
    <h2>INGRESAR</h2>
    <form @submit.prevent="login">
      <input v-model="usuario" type="text" placeholder="Usuario">
      <input v-model="contrasena" type="password" placeholder="Contraseña">
      <input type="submit" placeholder="Acceder">
    </form>
    <pre>
      {{$data}}
    </pre>
  </div>
</template>

<script>
import firebase from 'firebase';

export default {
      data() {
        return {
        usuario: '',
        contrasena: '',
        };
      },
      methods: {

        login() {
          firebase
          .auth()
          .signInWithEmailAndPassword(this.usuario, this.contrasena)
          .then((user) => this.$router.replace('home'), (error) => console.error(error));


        }
      }
};
</script>

<style scoped>
div {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

form > * {
  display: block;
}
</style>


