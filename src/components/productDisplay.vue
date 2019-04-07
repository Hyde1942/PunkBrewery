<template>
    <div>
        <display-items :stock="store.beerStock"></display-items>
    </div>
</template>


<script>
import productItem from './productItem.vue';
export default {
    data() {
        return { 
            store:{
                beerStock: [],
                stash:{
                    min:6,
                    max:12
                }
            }  
        }
    },
    components:{
        'display-items' : productItem
    },
    computed: {
        
    },
    methods: {
        randomNumber () {
            return Math.floor(Math.random() * (this.store.stash.max - this.store.stash.min + 1)) + this.store.stash.min;
        }
    },
    created() {
        console.log('component created');
        let page = this.randomNumber(), per_page = this.randomNumber() * 2;
        const url = `https://api.punkapi.com/v2/beers?page=${page}&per_page=${per_page}`;
        axios.get(url).then(r => {
            let stash = r.data.map(beer =>{
                return Object.assign({qty:this.randomNumber()},beer); 
            });
            this.store.beerStock = stash;
            console.log('Stock: ', this.store.beerStock);
        });
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
