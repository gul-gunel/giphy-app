<template>
	<div>
		<ul>
			<li v-for="(gif, index) in gifs" :key="index">
				<img :src="gif.images.fixed_height.url" alt="">
			</li>
		</ul>
	</div>
</template>
<script>
export default {
	props: ['gifs'],
}
</script>
<style>	
	li {
		list-style: none;
		float: left;
		margin: 20px;
	}	
</style>
