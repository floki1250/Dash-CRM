<template>
  <q-page
    class="flex flex-center"
    style="background-color: #DFE5E5;min-width:512px"
  >
    <div id="bg"></div>
  </q-page>
</template>

<script>
import anime from "animejs";

export default {
  name: "Profile",
  data() {
    return {};
  },
  methods() {
    anime({
      targets: "#bg",
      scale: [
        { value: 0.1, easing: "easeOutSine", duration: 500 },
        { value: 1, easing: "easeInOutQuad", duration: 1200 }
      ],
      delay: anime.stagger(200, { grid: [14, 5], from: "center" })
    });
  },
  mounted() {
    this.anime();
  }
};
</script>
<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@200&display=swap");
h2 {
  font-family: "Montserrat", sans-serif;
}
.bg {
  width: 500px;
  color: #000;
  background: red;
}
</style>
