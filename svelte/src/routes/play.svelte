<script>
	import Bar from '$lib/Bar.svelte';
	import WalletConnect from '$lib/WalletConnect.svelte';
	const contractAddr = '0xcE0Ef4bd15607f48828a254e8188A3cE567D2ceE';
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
	<div class="flex flex-col items-center">
		<PlayGotchi {web3Props} contractAbi={EmojiGotchiAbi} />
	</div>
{/if}
