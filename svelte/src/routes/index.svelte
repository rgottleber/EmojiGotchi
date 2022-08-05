<script>
	import EmojiGotchi from '$lib/EmojiGotchi.svelte';
	const contractAddr = '0xf21DcA0DD4758bD54f08e0Fc763ec53af9fDba06';
	const url = 'https://api.avax-test.network/ext/bc/C/rpc';
</script>

<h1>My EmojiGotchi</h1>

<EmojiGotchi {contractAddr} {url} />
