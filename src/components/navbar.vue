<template>
    <div>
        <nav>
            <ul>
                <li v-for="(page, index) in navList" :key="index">{{page}}</li>
            </ul>
        </nav>
    </div>
</template>

<script>
export default {
    data() {
        return {
            navList:[
                'home',
                'store',
                'shopping cart',
                'contact'
            ]
        }
    }
}
</script>

<style scoped>

</style>
