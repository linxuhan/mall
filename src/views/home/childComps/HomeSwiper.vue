<template>
  <swiper ref="swiper" v-if="banners.length">
		<swiper-item v-for="(item, index) in banners" :key="index">
			<a :href="item.link">
				<img :src="item.image" alt="" @load="imageLoad">
			</a>
		</swiper-item>
	</swiper>
</template>

<script>
import { Swiper, SwiperItem } from 'common/swiper'

export default {
	name: 'HomeSwiper',
	components: {
		Swiper,
		SwiperItem
	},
	props: {
		banners: {
			type: Array,
			default: []
		}
	},
	data() {
		return {
			isLoad: false
		}
	},
	methods: {
		stopTimer() {
			this.$refs.swiper.stopTimer()
		},
		startTimer() {
			this.$refs.swiper.startTimer()
		},
		imageLoad() {
			if (!this.isLoad) {
				console.log("--11")
				this.$emit('swiperImageLoad')
				this.isLoad = true
			}
		}
	}
}
</script>

<style>

</style>