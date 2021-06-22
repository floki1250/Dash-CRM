<template>
  <q-layout view="hHh lpR fFf">
    <q-drawer
      show-if-above
      v-model="left"
      side="left"
      behavior="desktop"
      elevated
      content-class="bg-listheadertoolbar"
    >
      <!-- drawer content -->
      <div class="title-logo">
        <div><img src="~assets/logo.svg" alt="" /></div>
        <p>Dash CRM</p>
      </div>
      <q-list padding>
        <q-item to="home" clickable class="item">
          <q-item-section avatar>
            <q-icon name="las la-home" />
          </q-item-section>
          <q-item-section>
            Home
          </q-item-section>
        </q-item>
        <q-item to="profile" clickable class="item">
          <q-item-section avatar>
            <q-icon name="las la-user" />
          </q-item-section>
          <q-item-section>
            Profile
          </q-item-section>
        </q-item>
        <q-item clickable class="item" @click="settings = true">
          <q-item-section avatar>
            <q-icon name="las la-cog" />
          </q-item-section>
          <q-item-section>
            Settings
          </q-item-section>
        </q-item>
        <q-item @click="toolbar = true" clickable class="item">
          <q-item-section avatar>
            <q-icon name="las la-info-circle" />
          </q-item-section>
          <q-item-section>
            About Us
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
    <q-dialog v-model="toolbar">
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
            <img
              src="https://scontent.ftun16-1.fna.fbcdn.net/v/t1.6435-9/169409593_5207942349281246_8392409286670678548_n.jpg?_nc_cat=100&ccb=1-3&_nc_sid=09cbfe&_nc_ohc=3shv-S2XfdoAX_OV46a&_nc_ht=scontent.ftun16-1.fna&oh=5bf886529f79bf9ce1947a039890a376&oe=60D0AA8D"
              alt=""
            />
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
    </q-dialog>
    <q-dialog v-model="settings">
      <q-card class="my-card">
       
        <q-card-section>
          
         <q-toggle  color="grey" keep-color unchecked-icon="las la-sun" checked-icon="las la-moon" size="50px"/>
        </q-card-section>
      </q-card>
    </q-dialog>
  </q-layout>
</template>

<script>

export default {
  methods: {
    opentab: function(url) {
      window.open(url);
    }
  },
  data() {
    return {
      settings: false,
      show: false,
      left: true,
      toolbar: false
    };
  }
};
</script>
