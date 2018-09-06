<template>
<div>
  <nav class="navbar navbar-dark bg-primary">
      <a class="navbar-brand" href="#" @click="logout">Salir</a>
  </nav>
  <!-- CONTENIDO PRINCIPAL -->
  <div class="container">
    <div class="row mt-5">
      <div class="col-sm-4">
        <div class="card">
          <div class="card-header">
            <h3>Ingresa un Alumno</h3>
          </div>
          <div class="card-body">
            <form @submit.prevent="addAlumno">
              <div class="form-group">
                <input type="text" class="form-control" v-model="newAlumno.nombre" placeholder="Nombre del Alumno">
              </div>
              <div class="form-group">
                <input type="text" class="form-control" v-model="newAlumno.grupo" placeholder="Grupo">
              </div>
              <div class="form-group">
                <input type="text" class="form-control" v-model="newAlumno.lista" placeholder="No. de Lista">
              </div>
               <button type="submit" class="btn btn-primary">
                  Guardar
                </button>
            </form>
          </div>
        </div>

      </div>
      <div class="col-sm-8 text-center">
        <div class="card">
          <div class="card-header">
            <h3>Listado de Alumnos</h3>
          </div>
          <div class="card-body">
            <table class="table table-striped table-bordered">
              <thead>
                <tr>
                  <th>No. de Lista</th>
                  <th>Nombre</th>
                  <th>Grupo</th>
                  <th>Acciones</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="alumno in alumnos" :key="alumno.lista">
                  <td>
                    {{ alumno.lista }}</td>

                  <td><button class="btn btn-danger">Borrar</button></td>
                </tr>
              </tbody>

            </table>
          </div>
        </div>
      </div>
    </div>
  </div>

    <pre>
      {{$data}}
    </pre>

</div>

</template>

<script>
import firebase from 'firebase'
import config from '../config'
var app = firebase.initializeApp(config);
var db = app.database();
var alumnosRef = db.ref('alumnos')

export default {
  name: 'HelloWorld',
  firebase: {
    alumnos: alumnosRef
  },

  data () {
    return {
     newAlumno: {
       lista: '',
       nombre: '',
       grupo: ''
     }
    }
  },
  methods: {
    logout() {
      firebase.auth().signOut().then(()=> this.$router.replace('login'))
    },

    addAlumno()  {
      alumnosRef.push(this.newAlumno)
      this.newAlumno.lista = ''
      this.newAlumno.nombre = ''
      this.newAlumno.grupo = ''
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
