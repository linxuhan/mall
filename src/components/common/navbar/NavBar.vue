<template>
  <div id="nav-bar">
		<div class="left"><slot name="left"></slot></div>
		<div class="center"><slot name="center"></slot></div>
		<div class="right"><slot name="right"></slot></div>
	</div>
</template>

<script>
	export default {
		name: "NavBar"
	}
</script>

<style scoped>
	#nav-bar {
		position: relative;
		display: flex;
		z-index: 10;
		height: 44px;
		line-height: 44px;
		text-align: center;
	}
	.left, .right {
		width: 60px;
	}
	.center {
		flex: 1;
	}
</style>