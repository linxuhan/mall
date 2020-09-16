<template>
  <div id="swiper">
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
		}
	}
</script>

<style>

</style>