<script>
	import EmojiGotchi from '$lib/EmojiGotchi.svelte';
	const contractAddr = '0xcE0Ef4bd15607f48828a254e8188A3cE567D2ceE';
	const url = 'https://rpc-mumbai.maticvigil.com';
</script>

<!-- tailwind center items in column with flex  -->
<div class="flex flex-col items-center">
	<h1 class="text-6xl">Our EmojiGotchi</h1>

	<EmojiGotchi {contractAddr} {url} />
</div>
