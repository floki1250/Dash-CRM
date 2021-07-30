<template>
  <div>
    <span class="clock"> {{ timestamp }}</span>
  </div>
</template>
<script>
export default {
  template: "#timestamp",

  data() {
    return {
      timestamp: ""
    };
  },
  created() {
    setInterval(this.getNow, 1000);
  },
  methods: {
    getNow() {
      const today = new Date();
      const time =
	  (today.getHours() < 10 ? "0" : "")+
        today.getHours() +
        ":" +
        (today.getMinutes() < 10 ? "0" : "") +
        today.getMinutes() +
        ":" +
        (today.getSeconds() < 10 ? "0" : "") +
        today.getSeconds() +
        "  " +
        (today.getHours() > 12 ? "PM" : "AM");
      this.timestamp = time;
    }
  }
};
</script>
<style></style>
