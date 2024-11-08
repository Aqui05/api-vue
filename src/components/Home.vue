<template>
    <div class="contain">
        <Header />
        <h1>Home Component</h1>
    </div>
</template>

<script>
import Header from './Header.vue';

    export default {
        name: "Home",
        components: {
            Header
        },
        mounted() {
            let user=localStorage.getItem("user-info");
            if(!user) {
            this.$router.push({name:'login'});
            }
        }
    }
</script>