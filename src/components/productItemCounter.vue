<template>
    <div>
        <button @click="add">+</button>
        <span>{{counter}}</span>
        <button @click="remove">-</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            counter: 0
        }
    },
    props:{

    },
    methods: {
        add(){
            return this.counter++
        },
        remove (){
            return  this.counter > 0 ? this.counter-- : 0;
        }
    },
    computed: {
        
    },
}
</script>


<style scoped>

</style>

