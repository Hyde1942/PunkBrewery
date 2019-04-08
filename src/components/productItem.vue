<template>
    <div>
       <div id="product-idx" data-id="idx" v-for="(beer, idx) in stock" :stock="stock" :key="idx" class="beers">
           <div class="img-wrapper-outer">
            <div class="img-wrapper-inner">
                <img :src="beer.image_url" alt="beer.name">
            </div>
           </div>
           <div class="product-description">
             <h2>{{beer.name}} - {{beer.abv}}%</h2>
             <p>{{beer.tagline}}</p>
             <p>{{beer.description}}</p>
             <p>{{beer.brewers_tips}}</p>
             <ul>
                <li v-for="(food, i) in beer.food_pairing" :key="i">{{food}}</li>
            </ul>
            <p>In Stock: {{beer.qty}}</p>
            <add-cart :item="beer.name" v-on:shopList="checkout" :inStockQty="beer.qty"></add-cart>        
           </div>
       </div>
    </div>
</template>


<script>

import cart from './productAddToCart.vue';

export default {
    props:['stock'],
    data() {
        return { 
          shoppingList: [],
        }
    },
    components: {
        'add-cart': cart
    },
    methods: {
        checkout (obj){
            this.shoppingList.push(obj);
            this.$emit('checkout',this.shoppingList);
            this.shoppingList.pop();
        }
    }
}
</script>

<style scoped>

/* 
  font-family: 'Paytone One', sans-serif;
  font-family: 'Pattaya', sans-serif;
  font-family: 'Aclonica', sans-serif;
  font-family: 'Signika', sans-serif;
  font-family: 'Cuprum', sans-serif;
 */

.beers {
    display: flex;
    margin-bottom: 1em;
}
.beers .img-wrapper-outer {
    width: 20%;
    text-align: center;
    background-color: cyan;
    overflow: hidden;
    padding:2em;
}

.beers .img-wrapper-inner {
    width:40%;
    margin:0 auto;
}

.beers .img-wrapper-inner img {
    max-width: 100%;
    vertical-align: middle
}

.beers .product-description {
    width:80%;
    background-color: darkmagenta;
    color:white;
    text-shadow: -2px 1px 0px black;
    padding:2em;
}
.beers h2 { 
    font-family: 'Signika', sans-serif;
}
.beers p, .beers ul {
    font-family: 'Cuprum', sans-serif;
    font-size: 1.5em;
}

</style>

