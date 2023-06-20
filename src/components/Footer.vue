<template>
    <footer id="footer">
        <p>FM Burger &copy; 2023</p>
    </footer>
</template>

<script>
export default {
    name: "Footer",
};
</script>

<style scoped>
#footer {
    background-color: #222;
    border-top: 4px solid #111;
    color: #fcba03;
    display: flex;
    align-items: center;
    justify-content: center;
    max-width: 100%;
}

p {
    margin: 0 7%;
    text-align: center;
    width: 86%;
    padding: 2% 5%;
}
</style>
