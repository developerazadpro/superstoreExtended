<template>
    <div v-if="!loading" class="row">
        <div v-for="(item, index) in items" :key="index" class="card" style="width: 15rem;">
            <img :src="item.photo" class="card-img-top" alt="cart-img">
            <div class="card-body">
            <h5 class="card-title">{{ item.title }}</h5>
            <p class="card-text">${{ item.price }}</p>
            <a @click="addItemToCart(item)" class="btn btn-primary text-white">Add to Cart</a>
            </div>
        </div>
    </div>
    <div v-else class="row">
        <h3>Loading...</h3>
    </div>
</template>

<script>

import axios from 'axios'
export default {
    data(){
        return {
            loading: true,
            items: []
        }
    },
    mounted() {
        this.fetchInventory()
    },
    methods:{
        addItemToCart(item){
            this.$emit('newItemAdded', item)
        },
        fetchInventory(){
            var self = this
            axios.get('http://localhost:3000/items').then(response => {
                setTimeout(function(){
                    self.items = response.data
                    self.loading = false
                }, 3000)                
            })
        }
    }
}
</script>

<style>

</style>