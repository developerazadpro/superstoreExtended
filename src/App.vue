<template>
  <div id="app">
      
      <router-link :to="{path: '/'}">Home</router-link>
      <router-link :to="{path: '/test'}">Test</router-link>
      
      <router-view></router-view>
      <!--
      <Navbar @search='search'></Navbar>

      <div class="container">
        <div class="row">
            <div class="col-sm-9">
                <Inventory @newItemAdded='addCartItem' :items="items"></Inventory>
            </div>
            <div class="col-sm-3 card-item">
                <Cart @removeItem='removeItem' :items="cart"></Cart>
            </div>
        </div>        
      </div>
      -->
  </div>
</template>

<script>
  import Navbar from './components/Navbar'
  import Inventory from './components/Inventory'
  import Cart from './components/Cart'
  import data from './data.js'

  export default {
    name: 'app',

    components:{
      Navbar,
      Inventory,
      Cart
    },

    data(){
      return{
        items: [],
        cart:[]
      }
    },

    mounted(){
      this.items = data
    },

    methods:{
      search(keyword){
        this.items = data.filter(item =>{
          return item.title.toLowerCase().indexOf(keyword.toLowerCase()) !== -1
        })
      },
      addCartItem(item){
        this.cart.push(item)
      },
      removeItem(index){
        this.cart.splice(index, 1)
      }
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }
  .container, .card-item{
    padding-top: 10px;
  }
  .card{
    margin:10px;
  }
  

  @import'~bootstrap/dist/css/bootstrap.css'
</style>