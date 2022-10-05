<script>
	export let url;
</script>

<div class="render" style={`background: #fff url(${url}) center center/cover no-repeat`} />

<style>
	.render {
		display: block;
		height: 100%;
		width: 100%;
		position: fixed;
		z-index: 0;
	}
</style>
