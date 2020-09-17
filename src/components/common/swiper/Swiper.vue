<template>
  <div id="swiper">
		<!-- <div class="swiper" @touchstart="touchStart" @touchmove="touchMove" @touchend="touchEnd"> -->
		<div class="swiper" @touchstart="touchStart" @touchmove="touchMove" @touchend="touchEnd">
			<slot></slot>
		</div>
		<slot name="indicator"></slot>
		<div class="indicator">
			<slot name="indicator" v-if="showIndicator && slideCount > 1">
				<div v-for="(item, index) in slideCount" class="indi-item" :class="{ active: index === currentIndex - 1 }" :key="index"></div>
			</slot>
		</div>
	</div>
</template>

<script>
	export default {
		name: "Swiper",
		props: {
			interval: {
				type: Number,
				default: 3000
			},
			animDuration: {
				type: Number,
				default: 300
			},
			moveRatio: {
				type: Number,
				default: 0.25
			},
			showIndicator: {
				type: Boolean,
				default: true
			}
		},
		data() {
			return {
				slideCount: 0,
				totalWidth: 0,
				swiperStyle: {},
				currentIndex: 1,
				scrolling: false
			}
		},
		mounted() {
			// 1.操作DOM, 在前后添加Slide
			setTimeout(() => {
				this.handleDom()
				this.statrTimer()
			}, 3000)
		},
		methods: {
			statrTimer() {
				this.playTimer = window.setInterval(() => {
					this.currentIndex++
					this.scrollContent(-this.currentIndex * this.totalWidth)
				}, this.interval)
			},
			stopTimer() {
				window.clearInterval(this.playTimer)
			},
			scrollContent(currentPosition) {
				this.scrolling = true
				this.swiperStyle.transition = 'transform ' + this.animDuration + 'ms'
				// this.setTransform(currentPosition)
				// this.checkPosition()
				this.scrolling = false
			},
			handleDom() {
				let swiperEl = document.querySelector('.swiper')
				let slidesEls = swiperEl.getElementsByClassName('slide')
				this.slideCount = slidesEls.length
				if (this.slideCount > 1) {
					let cloneFirst = slidesEls[0].cloneNode(true)
					let cloneLast = slidesEls[this.slideCount - 1].cloneNode(true)
					swiperEl.insertBefore(cloneLast, slidesEls[0])
					swiperEl.appendChild(cloneFirst)
					this.totalWidth = swiperEl.offsetWidth
					this.swiperStyle = swiperEl.style
				}
				// this.setTransform(-this.totalWidth)
			}
		}
	}
</script>

<style scoped>

</style>