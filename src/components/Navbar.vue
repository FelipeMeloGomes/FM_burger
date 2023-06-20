<template>
    <div id="nav">
        <router-link to="/" id="logo-url">
            <img :src="logo" :alt="alt" id="logo" />
        </router-link>
        <div id="links">
            <router-link to="/">Home</router-link>
            <router-link to="/pedidos">Pedidos</router-link>
        </div>
    </div>
</template>
<script>
export default {
    name: "Navbar",
    props: ["logo", "alt"],
};
</script>
<style scoped>
#nav {
    background-color: #222;
    border-bottom: 4px solid #111;
    padding: 2% 5%;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

#nav #logo-url {
    margin-left: 0;
}

#logo {
    width: 40px;
    height: 40px;
}

#links {
    display: flex;
    flex-wrap: wrap;
    justify-content: flex-end;
    align-items: center;
}

#nav a {
    color: #fcba03;
    text-decoration: none;
    margin: 12px;
    transition: 0.5s;
}

#nav a:hover {
    color: #fff;
}

@media screen and (max-width: 768px) {
    #nav {
        flex-direction: column;
        align-items: flex-start;
    }

    #links {
        margin-top: 20px;
        justify-content: flex-start;
    }
}
</style>
