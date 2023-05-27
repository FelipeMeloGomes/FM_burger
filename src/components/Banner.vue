<template>
  <div id="main-banner">
    <h1>FM Burger</h1>
  </div>
</template>

<script>
export default {
  name: "Banner",
};
</script>

<style scoped>
#main-banner {
  background-image: url("/public/img/burger.jpg");
  background-size: cover;
  height: 70vh;
  display: flex;
  align-items: center;
  justify-content: start;
}

#main-banner h1 {
  display: flex;
  color: #fff;
  text-align: center;
  font-size: 5vw;
  background-color: #222;
  padding: 2vw 4vw;
}

@media (min-width: 990px) {
  #main-banner {
    background-position: 0 -250px;
  }
}

@media (max-width: 768px) {
  #main-banner {
    height: 40vh;
    background-position: 0 -126px;
  }

  #main-banner h1 {
    font-size: 5vw;
  }

  @media (max-width: 630px) {
    #main-banner {
      background-position: 0;
    }
  }
}
</style>
