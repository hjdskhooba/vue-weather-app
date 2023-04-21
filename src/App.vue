<template>
    <h1 style="text-align: center;" @click="log">{{ hello }}</h1>
</template>
<script>
export default {
    data(){
        return {
            hello: "Hello world"
        }
    },
    methods: {
        log(event){
            alert(event.target.innerText)
        }
    },
}
</script>
<style>
    h1{
        width: 100%;
        font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
        font-weight: 400;
        font-style: normal;
        font-stretch: condensed;
    }
</style>