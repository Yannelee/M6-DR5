<template>
  <div>
    <div class="personal__info">
      <button class="btn btn-warning" @click="signIn" v-show="addUser">Ingresar</button>
      <div class="showUser m-2" v-show="user">
        <div class="alert w-75 m-auto" role="alert">
          <h3 class="alert-heading">Bienvenidx {{getFullName}}</h3>
          <p class="mb-0">Elige la película que deseas para conocer su información.</p>
        </div>
          <button class="btn btn-warning m-2" @click="clearUser">Limpiar Usuario</button>
      </div>
    </div>

    <div>
      <select name="ghibliMovies" id="ghibliMovies" @change="cambio($event)" v-show="user" class="p-1">
        <option disabled selected>Selecciona</option>
        <option v-for="(peli) in info" :key="peli.title">{{peli.title}}</option>
      </select>
      <div class="movieSelected" v-show="movieSelected">
        <div class="card m-3 mx-auto">
          <div class="row">
            <div class="col-md-4">
              <img :src="movieInfo.poster" class="rounded-start img-movie" :alt="movieInfo.title">
            </div>
            <div class="col-md-8">
              <div class="card-body">
                <h3 class="card-title">{{movieInfo.title}}</h3>
                <small><b>Titulo Romanizado</b></small>
                <p class="card-text">{{movieInfo.hepburn}}</p>
                <small><b>Director</b></small>
                <p class="card-text">{{movieInfo.director}}</p>
                <small><b>Sinopsis</b></small>
                <p class="card-text">{{movieInfo.synopsis}}</p>
                <small><b>Duración</b></small>
                <p class="card-text">{{movieInfo.runtimeMinutes}} Minutos</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  <div class="footer p-1"> Created by: Yannelee ✨</div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: "ghibli-component",
  data:function(){
    return{
      nombre:'',
      apellido:'',
      info:[],
      user: false,
      addUser: true,
      movieIndex:'',
      movieSelected: '',
      movieInfo:'',
      regex: /[a-zA-Z]/,
    }
  },
  methods:{
    signIn(){
      this.nombre = prompt('Ingresa tu nombre')
      this.apellido = prompt('Ingresa tu apellido')
      console.log(this.regex.test(this.nombre));
      if(this.regex.test(this.nombre) && this.regex.test(this.apellido)){
        this.user = true
        this.addUser = false
      } else {
        alert('Debes ingresar un Nombre y Apellido Válido')
      }
    },
    cambio(event){
      this.movieSelected = event.target.value
      this.movieIndex = Object.keys(this.info).findIndex(e => e == this.movieSelected.toLowerCase())
      this.movieInfo =Object.values(this.info)[this.movieIndex]
      if(this.movieSelected){
        this.movieSelected = true
      }
    },
    clearUser(){
      this.nombre =''
      this.apellido = ''
      this.user = false
      this.addUser = true
      this.movieSelected = false
    }
  }, 
  created () {
    axios
      .get('https://studio-ghibli-films-api.herokuapp.com/api/')
      .then(response => this.info = response.data)
  },
  computed:{
    getFullName(){
      return `${this.nombre} ${this.apellido}`
    },
  },
}
</script>

<style>
.alert{
  background-color: #ffffffef;
  border: .2rem solid white;
  border-radius: 2rem;
}
#ghibliMovies{
  width: 70%;
}
.card{
  background-color: #ffffffef;
  width: 80%;
}
.card-body{
  text-align: left;
}
.col-md-4{
  width: 30%;
  text-align: left;
}
.img-movie{
  height: 100%;
  max-width: 100%;
}
.footer{
  position: fixed;
  bottom: 0;
  width: 100%;
  background-color: white;
}
</style>