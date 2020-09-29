<template>
  <div ref="wrapper">
		<slot></slot>
	</div>
</template>

<script>
	import BScroll from 'better-scroll'

	export default {
		name: "Scroll",
		data() {
			return {
				scroll: null
			}
		},
		mounted() {
			this.scroll = new BScroll(this.$refs.wrapper, {
				click: true
			})
			this.scroll.scrollTo(0, 0)
		},
		methods: {
			scrollTo(x, y, time=500) {
				this.scroll.scrollTo(x, y, time)
			}
		}
	}
</script>

<style>

</style>