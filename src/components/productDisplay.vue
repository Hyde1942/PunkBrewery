<template>
    <div>
        <display-items :stock="store.beerStock"></display-items>
    </div>
</template>


<script>
import displayItems from './displayItems.vue';
export default {
    data() {
        return { 
            store:{
                beerStock: []
            }  
        }
    },
    components:{
        'display-items' : displayItems
    },
    computed: {
        
    },
    created() {
        console.log('component created');
        const url = 'https://api.punkapi.com/v2/beers?page=10&per_page=10';
        axios.get(url).then(r => {

            this.store.beerStock = r.data;
        });
     console.log('Beers Loaded');
     console.log(this.store.beerStock)
    },
    mounted() {
        console.log('component Mounted');
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
