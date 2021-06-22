<template>
  <q-page class="flex flex-center" style="background-color: #DFE5E5;min-width:512px">
   
      <div style="">
        <q-avatar size="128px">
          <img src="~/assets/avatar.png" alt="" />
        </q-avatar>
      </div>
      <div class="col-6">
        <h2 style="color:#363740;">
          My Profile
        </h2>
      </div>
       <div class="row" style="margin:20px">
          <div style="width:fit-content;">
        <img src="~/assets/profile.png" alt="" width="512" />
      </div>
      <div>
        <q-form class="q-gutter-md">
          <q-input
            rounded
            outlined
            lazy-rules
            :rules="[val => (val && val.length > 0) || 'Please type something']"
            dense
            value="username"
            hint="Username"
          />
          <q-input
            type="password"
            dense
            rounded
            outlined
            value="Floki1250"
            hint="Password"
            lazy-rules
            :rules="[val => (val && val.length > 0) || 'Please type something']"
          />
          <q-input
            dense
            type="number"
            value="25"
            rounded
            outlined
            hint="Age"
            :rules="[
              val => (val !== null && val !== '') || 'Please type your age',
              val => (val > 0 && val < 100) || 'Please type a real age'
            ]"
          />

          <div>
            <q-btn
              label="Save"
              type="submit"
              color="secondary"
              rounded
              icon="las la-save"
            />
          </div>
        </q-form>
      </div>
     
    </div>
  </q-page>
</template>

<script>
export default {
  name: "Profile",
  data() {
    return {
      name: null,
      age: null,
      password: null,

      accept: false
    };
  }
};
</script>
<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@200&display=swap");
h2 {
  font-family: "Montserrat", sans-serif;
}
</style>
