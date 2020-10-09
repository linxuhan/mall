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
		props: {
			probeType: {
				type: Number,
				default: 0
			},
			pullUpLoad: {
				type: Boolean,
				default: false
			}
		},
		mounted() {
			this.scroll = new BScroll(this.$refs.wrapper, {
				click: true,
				probeType: this.probeType,
				pullUpLoad: this.pullUpLoad
			})

			if (this.probeType === 2 || this.probeType === 3) {
				this.scroll.on('scroll', (position) => {
					// console.log(position)
					this.$emit('scroll', position)
				})
			}

			if (this.pullUpLoad) {
				this.scroll.on('pullingUp', () => {
					console.log("上拉加载更多")
					this.$emit('pullingUp')
				})
			}
		},
		methods: {
			scrollTo(x, y, time=500) {
				this.scroll && this.scroll.scrollTo(x, y, time)
			},
			refresh() {
				console.log("----")
				this.scroll && this.scroll.refresh && this.scroll.refresh()
			}
		}
	}
</script>

<style>

</style>