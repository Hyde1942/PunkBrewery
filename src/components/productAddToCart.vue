<template>
    <div>
        <label for="addToCart">Purchase Beers </label>
        <input id="addToCart" v-model="beerQty" @keyup.enter="checkInput" value="beerQty"  type="number" min="0" :max="inStockQty"/>
        <a v-show="beerQty > 0" @mouseenter="enterHover" @click.prevent="addToCart(item,beerQty)" class="btn-6" href="#">Add To Cart<span></span></a>
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
     },
     enterHover (e) {
        console.log(e);
         let parentOffset = e.target.offsetParent,
         relX = e.pageX - parentOffset.left,
         relY = e.pageY - parentOffset.top,
         child = e.target.childNodes[1];
         child.style.positionTop = relY;
         child.style.positionLeft = relX;
     }
    },
    computed: {
        
    },
}
</script>


<style scoped>

label,button {
    font-family: 'Cuprum', sans-serif;
    font-size: 1.5em;
}

input[type="number"] {
    font-family: 'Cuprum', sans-serif;
    color:white;
    background-color: black;
    border:2px solid white;
    text-align: center;
    padding:0.25em;
    border-radius:15px;
    font-size: 1em;
    margin-left: 0.5em;
    height: 2em;

}

[class^=btn-] {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  width: 210px;
  height: 60px;
  text-transform: uppercase;
  border: 1px solid currentColor;
}

.btn-6 {
  color: #31b462;
}
.btn-6 span {
  position: absolute;
  display: block;
  width: 0;
  height: 0;
  border-radius: 50%;
  background-color: #08642a;
  transition: width 0.4s ease-in-out, height 0.4s ease-in-out;
  transform: translate(-50%, -50%);
  z-index: -1;
}
.btn-6:hover {
  color: #c3e9d1;
}
.btn-6:hover span {
  width: 225%;
  height: 562.5px;
}
.btn-6:active {
  background-color: #0da746;
}


</style>

