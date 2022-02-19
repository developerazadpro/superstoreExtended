<template>
    <div class="row">
        <div v-for="(item, index) in items" :key="index" class="card" style="width: 15rem;">
            <img :src="item.photo" class="card-img-top" alt="cart-img">
            <div class="card-body">
            <h5 class="card-title">{{ item.title }}</h5>
            <p class="card-text">${{ item.price }}</p>
            <a @click="addItemToCart(item)" class="btn btn-primary text-white">Add to Cart</a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    //props:['items'],
    data(){
        return {
            items: []
        }
    },
    methods:{
        addItemToCart(item){
            this.$emit('newItemAdded', item)
        }
    }
}
</script>

<style>

</style>