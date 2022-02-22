<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">    
      <router-link class="navbar-brand" :to="{path:'/'}">Super Store</router-link>    
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav mr-auto">
            <li class="nav-item active">
              <!--<a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>-->
            </li>
            
          </ul>
          <form @submit.prevent="search" class="form-inline my-2 my-lg-0">
            <input class="form-control mr-sm-2" type="search" v-model="keyword" placeholder="Search" aria-label="Search">
            <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
          </form>
        </div>
     </nav>
</template>

<script>
import axios from 'axios'
export default {
    data() {
      return {
        keyword:''
      }
    },
    methods: {
      search() {
        var self = this
        axios.get('http://localhost:3000/search/' + this.keyword).then( response => {
           self.$store.commit('setInventory', response.data) 
        })
      }
    }
}
</script>

<style>

</style>