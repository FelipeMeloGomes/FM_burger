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
            logo_src: "/img/logo.png",
            app_name: "Fm burger",
        };
    },
};
</script>


<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");
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
