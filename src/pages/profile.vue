<template>
  <q-page
    class="flex flex-center"
    style="background-color: #DFE5E5;min-width:512px"
  >
    <q-card>
        <q-toolbar>
          <q-toolbar-title
            ><span class="text-weight-bold">About Us</span></q-toolbar-title
          >
          <q-btn flat round dense icon="close" v-close-popup />
        </q-toolbar>
        <q-card-section style="margin-left:10px">
          <q-avatar
            size="200px"
            font-size="52px"
            color="grey"
            text-color="black"
            style="margin:20px;"
          >
            <img src="../assets/Brand.png" alt="" />
          </q-avatar>
          <q-separator />
          <p class="info">Hi 👋, I'm Floki Web Developer</p>
          <p class="info">For Any Support You can Find me Here</p>
          <div class="row">
           
            <q-btn
              @click="opentab('https://twitter.com/Adem1250_Dr')"
              flat
              round
              color="primary"
              icon="lab la-twitter"
              size="25px"
            />
            <q-btn
              @click="opentab('https://github.com/floki1250')"
              flat
              round
              color="black"
              icon="lab la-github"
              size="25px"
            />
            <q-btn
              icon="las la-envelope"
              color="black"
              size="25px"
              flat
              round
              @click="show = !show"
            ></q-btn>
            <p v-show="show" style="margin:25px" class="info">
              d.adem1250@gmail.com
            </p>
          </div>
          <q-btn
            flat
            rounded
            @click="opentab('https://www.discovertunisia.com/en/')"
            style="margin-left:10px"
            >Made with ❤️ in Tunisia</q-btn
          >
        </q-card-section>
      </q-card>
  </q-page>
</template>

<script>


export default {
  name: "Profile",
  data() {
    return {show: false,};
  },
  methods: {
    opentab: function(url) {
      window.open(url);
    },
  },
  
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
