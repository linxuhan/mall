<template>
  <div class="good">
		<good-list-item v-for="(item, index) in goodList" :key="index" :goods="item"></good-list-item>
	</div>
</template>

<script>
	import GoodListItem from './GoodListItem'

	export default {
		name: "GoodList",
		components: {
			GoodListItem
		},
		props: {
			goodList: {
				type: Array,
				default: []
			}
		}
	}
</script>

<style scoped>
	.good {
		display: flex;
		flex-wrap: wrap;
		justify-content: space-around;
	}
</style>