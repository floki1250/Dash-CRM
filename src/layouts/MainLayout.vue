<template>
  <q-layout view="hHh lpR fFf">
    <q-drawer
      v-model="drawer"
      show-if-above
      :mini="miniState"
      persistent
      content-class="bg-dark"
      :breakpoint="500"
    >
      <!-- drawer content -->

      <q-list padding>
        <q-item clickable v-ripple @click="State" class="title-logo">
          <q-item-section avatar>
            <img src="~/assets/logo.svg" alt="" />
          </q-item-section>
          <q-item-section>
            Dash CRM
          </q-item-section>
        </q-item>

        <q-item to="home" clickable class="item" v-ripple>
          <q-item-section avatar>
            <q-icon name="las la-home" />
          </q-item-section>
          <q-item-section>
            Home
          </q-item-section>
        </q-item>
        <q-item to="profile" clickable class="item" v-ripple>
          <q-item-section avatar>
            <q-icon name="las la-user" />
          </q-item-section>
          <q-item-section>
            Profile
          </q-item-section>
        </q-item>

        <q-item  clickable class="item" v-ripple>
          <q-item-section avatar>
            <q-icon name="las la-info-circle" />
          </q-item-section>
          <q-item-section>
            About Us
          </q-item-section>
        </q-item>

        <q-item clickable class="item" v-ripple >
          <q-item-section avatar>
            <q-icon name="las la-cog" />
          </q-item-section>
          <q-item-section>
            Settings
          </q-item-section>
          <!-- <Settings v-model="setting" />  -->
        </q-item>
      </q-list>
    </q-drawer>
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>



export default {
  data() {
    return {
      drawer: false,
      miniState: true,
      setting: false,
      
      toolbar: false
    };
  },
  methods: {
    
    opentab: function(url) {
      window.open(url);
    },
    State: function() {
      this.miniState = !this.miniState;
      /* document.getElementsByClassName("vue-highcharts").style.marginRight =
        "200px";
      console.log(document.getElementsByClassName("vue-highcharts")); */
    }
  },

  
  
  
};
</script>
