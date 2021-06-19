<template>
  <q-page class="flex flex-center" style="background-color: #DFE5E5;">
    
    <q-avatar size="128px" >
     <img src="~/assets/avatar.png" alt="">
    </q-avatar>
    <h1> My Profile</h1>
    <q-form
      class="q-gutter-md"
    >
    <q-input
        rounded outlined  label="Name"
        v-model="name"
        hint="Name"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type something']"
      />
  <q-input
  type="password"
        rounded outlined  label="Password"
        v-model="password"
        hint="Password"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type something']"
      />
      <q-input
        type="number"
        v-model="age"
        rounded outlined  label="Age"
        :rules="[
          val => val !== null && val !== '' || 'Please type your age',
          val => val > 0 && val < 100 || 'Please type a real age'
        ]"
      />

      <div>
        <q-btn label="Submit" type="submit" color="primary" rounded/>
        <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" rounded/>
      </div>
    </q-form>
    <div>
      <img src="~/assets/profile.png" alt="">
      </div>
  </q-page>
</template>

<script>
export default {
  name: "Profile" ,
  data () {
    return {
      name: null,
      age: null,
      password: null,

      accept: false
    }
  },
};
</script>
