<template>

<div class="container">
  
  <div class="row justify-content-center">
    
    <div class="col-12">

      <input type="text" class="form-control" name="" id="" placeholder="Buscar" v-model="search" @input="searchItems()">

    </div>

    <br>
    <br>
  
  <div v-if="!search" class="col-3" v-for="(item, index) in items">
      <div class="card" >
        <div class="card-header">
          <h4>{{ item.name }}</h4>
        </div>
      <div class="card-body">
        <div class="row">
          <div class="col-md-12">
            Lenguaje: <p>{{ item.default_language }}</p>
          </div>
        </div>
                <div class="row">
          <div class="col-md-12">
            Url: <p><a :href="item.homepage" target="_blank">{{ item.homepage }}</a></p>
          </div>
        </div>
    </div>
    </div>
  </div>

  <div v-else class="col-3" v-for="(item, index) in items">
      <div class="card" >
        <div class="card-header">
          <h4>{{ item.name }}</h4>
        </div>
      <div class="card-body">
        <div class="row">
          <div class="col-md-12">
            Lenguaje: <p>{{ item.language }}</p>
          </div>
        </div>
                <div class="row">
          <div class="col-md-12">
            Url: <p><a :href="item.homepage" target="_blank">{{ item.homepage }}</a></p>
          </div>
        </div>
    </div>
    </div>

  <br>
  
  </div>
  
  </div>
</div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import axios from "axios";


export default {
  name: 'HomeView',
  components: {
    HelloWorld
  },data() {
    return {
      title: 'Home',
      message: 'Welcome to your Vue.js + Vuetify application.',
      items: [],
      loading: false,
      search: '',
    }
  },methods: {
    getPosts() {
      axios.get('https://libraries.io/api/platforms')
      .then(response => {
        this.items = response.data;
      })
      .catch(error => {
        console.log(error);
      })
    },searchItems() {

      let me = this;

      if(!me.search) {
        me.getPosts();
      }
      
      axios.get('https://libraries.io/api/search?q='+this.search)
      .then(response => {
        console.log(this.search);

        me.items = response.data;
        console.log(response);
      })
      .catch(error => {
        console.log(error);
      })


    }
  },mounted() {
    this.getPosts();
  }
}
</script>
