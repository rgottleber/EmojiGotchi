<script>
	import Bar from '$lib/Bar.svelte';
	import WalletConnect from '$lib/WalletConnect.svelte';
	const contractAddr = '0xf21DcA0DD4758bD54f08e0Fc763ec53af9fDba06';
	import EmojiGotchiAbi from '../contracts/EmojiGotchi.json';
	import PlayGotchi from '../lib/PlayGotchi.svelte';

	export let web3Props = {
		provider: null,
		signer: null,
		account: null,
		chainId: null,
		contract: null
	};
</script>

{#if !web3Props.account}
	<WalletConnect bind:web3Props {contractAddr} contractAbi={EmojiGotchiAbi} />
{:else}
	<PlayGotchi {web3Props} contractAbi={EmojiGotchiAbi} />
{/if}

<style>
	div {
		width: 33%;
	}
</style>
