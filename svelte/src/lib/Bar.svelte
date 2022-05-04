<script>
	export let status;
</script>

<div class="status" style={`width: ${status}%;`} />

<style>
	.status {
		height: 8px;
		background: blue;
		opacity: 0.5;
		width: 33%;
	}
</style>
