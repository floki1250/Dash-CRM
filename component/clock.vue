<template>
  <div>
     <span class="clock" > {{ timestamp }}</span>
</div>
</template>
<script>
export default {
	
	template: '#timestamp',
	
	data() {
		return {
			timestamp: '',
		};
	},
	created() {
		setInterval(this.getNow, 1000);
	},
	methods: {
		getNow() {
			const today = new Date();
			const time =
				today.getHours() + ':' + (today.getMinutes() < 10 ? '0' : '') + today.getMinutes()+":" + today.getSeconds();
			this.timestamp = time;
		},
	},
};
</script>
<style>

</style>
