<template>
    <ul class="list-group">
        <li class="list-group-item">
            <span class="item-name"><b>Name</b></span>
            <span class="item-price float-right"><b>Price</b></span>
        </li>
        <hr>

        <li v-for="(item, index) in items" :key="index" class="list-group-item">
            <span class="item-name">{{ item.title }}</span>
            <span class="item-price float-right">${{ item.price }}  <button @click="removeItem(index)" class="btn btn-xs btn-danger">x</button></span>
            
        </li>
        <hr>
        <li class="list-group-item">
            <span class="item-name"><b>Total</b></span>
            <span class="item-price float-right"><b>${{ totalPrice }}</b></span>
        </li>

        <li v-if="items.length > 0" class="list-group-item">
            <button @click="checkout" class="btn btn-block btn-success text-white">Checkout</button>
        </li>
    </ul>
</template>

<script>
    export default {
        computed: {
            items(){
                return this.$store.getters.getCart
            },
            totalPrice(){
                var total = 0
                this.items.forEach(item => {
                    total += parseFloat(item.price)
                })
                return parseFloat(total).toFixed(2)
            }
        },
        methods:{
            removeItem(index){
                this.$store.commit('removeItem', index)
            },
            checkout(){
                if(confirm('Are you sure you want to checkout?')){
                    this.$store.commit('clearCart')
                }
            }
        }
    }
</script>

<style>
    .btn-xs {
        padding: .25rem .4rem;
        font-size: .875rem;
        line-height: .5;
        border-radius: .2rem;
    }
</style>