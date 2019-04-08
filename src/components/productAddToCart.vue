<template>
    <div>
        <input v-model="beerQty" @keyup.enter="checkInput" value="beerQty"  type="number" min="0" :max="inStockQty"/>
        <button v-show="beerQty > 0" @click="addToCart(item,beerQty)">Add To Cart</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            beerQty: 0,
            shoppingList: {
                name: '',
                 qty: 0,
                 orderID:''
            }
        }
    },
    props: {
        inStockQty: Number,
        item: String
    },
    methods: {
     addToCart(item, qty){
         if (this.beerQty > this.inStockQty) {
             return false;
         }else {
            this.shoppingList.name = item;
            this.shoppingList.qty = qty;
            this.$emit('shopList',this.shoppingList);
            this.beerQty = 0;
         }
     },
     checkInput() {
       if (this.beerQty > this.inStockQty) {
           return false;
       }
     }
    },
    computed: {
        
    },
}
</script>


<style scoped>

</style>

