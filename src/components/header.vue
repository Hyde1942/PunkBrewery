<template>
    <div>
       <header>
           <h1>{{header}}</h1>
       </header>
    </div>
</template>


<script>

export default {
    data() {
        return {
            header:'Brewing Company'       
        }
    }
}
</script>


<style>
    header {
        background-color:purple;
    }
    header h1 {
        margin:0 auto;
        color:white;
        padding: 0.5em 0;
        font-family: 'Aclonica', sans-serif;
        text-align: center;
        font-size: 3rem;
        border-bottom: 8px solid black;
        text-shadow: -4px 3px 0px black;
    }

    @media screen and (max-width: 767px) {
        header h1 {
            font-size: 2em;
        }
    }
</style>