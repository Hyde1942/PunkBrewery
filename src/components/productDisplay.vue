<template>
    <div>
        <display-items :stock="store.beerStock" v-on:checkout="checkout"></display-items>
    </div>
</template>


<script>
import productItem from './productItem.vue';
export default {
    data() {
        return { 
            store:{
                beerStock: [],
                orders: [],
                onQueue: 0,
                stash:{
                    min:6,
                    max:12
                }
            },
            empty: false  
        }
    },
    components:{
        'display-items' : productItem
    },
    watch: {
     empty () {
         this.fetchBeers();
         this.empty = false;
     }   
    },
    methods: {

        fetchBeers (){
            let page = this.randomNumber(), per_page = this.randomNumber() * 2;
            const url = `https://api.punkapi.com/v2/beers?page=${page}&per_page=${per_page}`;
            axios.get(url).then(r => {
            let stash = r.data.map(beer =>{
                return Object.assign({qty:this.randomNumber()},beer); 
            });
            this.store.beerStock = stash;
        });
        },
        randomNumber () {
            return Math.floor(Math.random() * (this.store.stash.max - this.store.stash.min + 1)) + this.store.stash.min;
        },
        checkout (shopList){
            let temp = shopList.map(item => {
                item.orderID = this.randomNumber() * 1245 * item.qty;
                return item
            });
            console.log('Processing Orders...!')
            this.store.orders.push(temp[0]);
            this.store.onQueue = this.store.orders.length;
            console.log('Orders on Queue...', this.store.onQueue);
            
            let removeOrder,
                removeItemStock;
            this.store.orders.forEach((order,idx) => {
                
                this.store.beerStock.forEach((beer,i) => {
                    if (beer.name.toLowerCase() === order.name.toLowerCase()) {
                        beer.qty = beer.qty - order.qty;
                        removeOrder = idx;
                    }
                    if(beer.qty === 0) {
                        removeItemStock = i;
                    }
                })
            })
            this.store.orders.splice(removeOrder);
            this.store.onQueue = this.store.orders.length;
            console.log('Stock remove', removeItemStock);

            if (removeItemStock >= 0) {
                this.store.beerStock.splice(removeItemStock,1);
                if (this.store.beerStock.length === 0){
                    this.empty = true;
                }
            }
        }
    },
    created() {
        console.log('component created');
        this.fetchBeers();
    },
    mounted() {

    },
    updated() {
        console.log('Component Updated');
    },
    destroyed() {
        console.log('Component Destroyed');
    },
}
</script>

<style>

</style>
