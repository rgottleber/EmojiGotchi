<script>
	import EmojiGotchi from '$lib/EmojiGotchi.svelte';
	import WalletConnect from '$lib/WalletConnect.svelte';
	import EmojiGotchiAbi from '../contracts/EmojiGotchi.json';
	const contractAddr = '0x1B75a2EeaeF63FEF0D36c5178f20324f24791e2D';

	export let web3Props = {
		provider: null,
		signer: null,
		account: null,
		chainId: null,
		contract: null
	};
</script>

<h1>My EmojiGotchi</h1>
{#if !web3Props.account}
	<WalletConnect bind:web3Props {contractAddr} contractAbi={EmojiGotchiAbi} />
{:else}
	<EmojiGotchi {web3Props} />
{/if}
