<template>
  <div v-if="item" class="row">
    <div class="col-sm-6">
       <img :src="item.photo" alt="Photo">
    </div>
    <div class="col-sm-6">
       <h4 class="text-left">{{ item.title }}</h4>
       <p class="text-justify"><b>Description:</b> {{ item.description }}</p>
       <p class="text-left">
         Price: ${{ item.price }} 
         <br><a @click="addToCart(item)" class="btn btn-primary text-white">Add to Cart</a>
         </p>

       
    </div>
  </div>
  <h3 v-else>Loading...</h3>
</template>

<script>
import axios from 'axios'
export default {
  data(){
    return{
      item: null
    }
  },
  mounted(){
    this.fetchItem()
  },
  methods:{
    fetchItem(){
      var self = this
      axios.get('http://localhost:3000/item/'+this.$route.params.id).then(response => {
        self.item = response.data
      })
    },
    addToCart(item){
      this.$store.commit('addToCart', item)
    }
  }
}
</script>


<style>

</style>
