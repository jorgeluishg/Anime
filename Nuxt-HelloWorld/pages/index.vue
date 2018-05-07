<template>

  <section class="container">
<!--
    <div>
      <logo/>
      <h1 class="title">
        Nuxt-HelloWorld
      </h1>
      <h2 class="subtitle">
        My impressive Nuxt.js project
      </h2>
      <div class="links">
        <a href="https://nuxtjs.org/" target="_blank" class="button--green">Documentation</a>
        <a href="https://github.com/nuxt/nuxt.js" target="_blank" class="button--grey">GitHub</a>
      </div>
    </div>
  -->
<div id="app">
   
    <h1>CRUD - Animes</h1>

    <form v-on:submit.prevent="addanime">
      <div class="row">
        <div class="col-md-6">
          <div class="form-group">
            <label>nombre:</label>
            <input type="text" class="form-control" v-model="anime.nombre"/>
          </div>
        </div>
        </div>

      <div class="row">
        <div class="col-md-6">
          <div class="form-group">
            <label>genero:</label>
            <input type="text" class="form-control" v-model="anime.genero"/>
          </div>
        </div>
        </div>

      <div class="row">
        <div class="col-md-6">
          <div class="form-group">
            <label>capitulos:</label>
            <input type="text" class="form-control" v-model="anime.capitulos"/>
          </div>
        </div>
        </div>

      <div class="row">
        <div class="col-md-6">
          <div class="form-group">
            <label>emision:</label>
            <input type="text" class="form-control" v-model="anime.emision"/>
          </div>
        </div>
        </div>
       
       <br />
        <div class="form-group">
          <button class="btn btn-primary">Create anime</button>
        </div>
      <br/>
           
    </form>
      <div class="form-group">

          <button @click="updateanime()">
              Update anime
          </button>
        </div>

  <ul v-if="posts && posts.length">
    <li v-for="anime of posts">
       {{ anime.id }} - 
       {{ anime.genero }}
              <button @click="getoneanime(anime.id)">
                edit
     </button>
     <button @click="deleteanime(anime.id)">
                delete
     </button>
    </li>
  </ul>

  <ul v-if="errors && errors.length">
    <li v-for="error of errors">
      {{error.message}}
    </li>
  </ul>
  </div>
  
</section>

</template>
<script>
// import HelloWorld from './components/HelloWorld.vue' 
import axios from 'axios';

export default {
  name: 'app',
  data() {
    return {
      anime: {},
      posts: [],
      errors: []
    }
  },
  created() {
    // Fetches posts when the component is created.
    this.getanimes();
 
  } ,
  methods: {
 
  getanimes() {
    axios.get('http://35.227.59.176:8081/api/animes')
    .then(response => {
      // JSON responses are automatically parsed.
      this.posts = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  },

  getoneanime(idanime) {
    axios.get('http://35.227.59.176:8081/api/animes'+ idanime)
    .then(response => {
      // JSON responses are automatically parsed.
      this.anime = response.data
      alert("status: " + response.status + ", selected: " + JSON.stringify(response.data));

    })
    .catch(e => {
      this.errors.push(e)
    })
  },

  addanime() {
    alert(this.anime.nombre + this.anime.nombre + this.anime.emision + this.anime.emision);
    axios.post('http://35.227.59.176:8081/api/animes',  this.anime)
    .then(response => {
      alert("status: " + response.status + ", inserted: " + JSON.stringify(response.data));
    })
    .catch(e => {
      this.errors.push(e)
    })
  },
  
  updateanime() {
    alert(idanime);
    alert(this.anime.id);
    axios.put('http://35.227.59.176:8081/api/animes' + this.anime.id,  this.anime)
    .then(response => {
      alert("status: " + response.status + ", updated: " + JSON.stringify(response.data));
      this.getAnimes();

    })
    .catch(e => {
      this.errors.push(e)
    })
  },
  

  deleteanime(idanime) {
    alert("delete" + idanime);
    
    axios.delete('http://35.227.59.176:8081/api/animes' + idanime)
    .then(response => {

      alert("status: " + response.status + ", deleted: " + JSON.stringify(response.data));
      this.getAnimes();

    })
    .catch(e => {
      this.errors.push(e)
    })
  },
  
  }

}
</script>

<style>
.container
{
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.title
{
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}
.subtitle
{
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}
.links
{
  padding-top: 15px;
}
</style>
