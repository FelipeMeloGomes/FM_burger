<template>
    <Navbar :logo="logo_src" :alt="app_name" />
    <router-view />
    <Footer />
</template>

<script>
// imports
import Navbar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";

export default {
    components: {
        Navbar,
        Footer,
    },
    data() {
        return {
            logo_src: "/img/logo.webp",
            app_name: "FM Burger",
        };
    },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@500,700&display=swap");

* {
    font-family: "Poppins";
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-weight: 500;
}

.main-container {
    min-height: 100vh;
}

h1 {
    margin-bottom: 3vw;
    text-align: center;
    color: #222;
}

@media screen and (min-width: 768px) {
    h1 {
        font-size: 2.625rem;
        margin-bottom: 1.875rem;
    }
}
</style>
