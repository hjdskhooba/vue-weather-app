<template>
  <Header :temp="temp"/>
  <Main @temp="onTemp"/>
  <Footer />
</template>
<script>
import Footer from "./Layout/Footer.vue";
import Header from "./Layout/Header.vue";
import Main from "./pages/Main.vue";

export default {
  data() {
    return {
        temp: "0°C"
    };
  },
  methods: {
    onTemp (data) {
        this.temp = data.temp
    } 
  },
  components: { Header, Footer, Main },
};
</script>
<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap");
* {
  -webkit-overflow-scrolling: touch;
  box-sizing: border-box;
  -webkit-user-select: none;
  -moz-user-select: none;
  user-select: none;
  -webkit-user-select: auto;
  font-family: Inter, sans-serif;
}
.container {
  max-width: 1920px;
  margin: 0 auto;
}
.wrapper {
  width: 100%;
  height: 100%;
}
</style>
