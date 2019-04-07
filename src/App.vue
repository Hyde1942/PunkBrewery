<template>
  <div id="App" class="liquor-store-wrapper">
   <header-section></header-section>
   <main>
     <products-section></products-section>
   </main>
   <footer-section></footer-section>
  </div>
</template>

<script>
import header from './components/header.vue';
import nav from './components/navbar.vue';
import footer from './components/footer.vue';
import products from './components/productDisplay.vue';


export default {
  name: 'app',
  data() {
     return {
        string: 'Liquor Store'
    }
  },
  components:{
    'header-section': header,
    'nav-bar': nav,
    'footer-section': footer,
    'products-section': products
  }

}
</script>

<style>

 body {
   background:black;
   margin: 0;
 }
</style>
