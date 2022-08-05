<script>
	import Bar from '$lib/Bar.svelte';
	import Face from '$lib/Face.svelte';

	export let web3Props = {
		provider: null,
		signer: null,
		account: null,
		chainId: null,
		contract: null
	};
	$: image = '';
	$: hunger = '';
	$: enrichment = '';
	$: happiness = '';
	$: tombstones = '';
	const getMyGotchi = async () => {
		let currentGotchi = await web3Props.contract.myGotchi();

		image = await currentGotchi[5];
		happiness = await currentGotchi[0].toNumber();
		hunger = await currentGotchi[1].toNumber();
		enrichment = await currentGotchi[2].toNumber();
		tombstones = await currentGotchi[3].toNumber();
		web3Props.contract.on('EmojiUpdated', async () => {
			currentGotchi = await web3Props.contract.myGotchi();
			image = await currentGotchi[5];
			happiness = await currentGotchi[0].toNumber();
			hunger = await currentGotchi[1].toNumber();
			enrichment = await currentGotchi[2].toNumber();
			tombstones = await currentGotchi[3].toNumber();
		});
	};
	getMyGotchi();
</script>

<div>
	<Face {image} />
</div>
<div>
	Hunger: {hunger}
	<br />
	<Bar bind:status={hunger} />
	<button
		on:click={() => {
			web3Props.contract.feed();
		}}>Feed</button
	>
</div>
<div>
	Enrichment: {enrichment}
	<br />

	<Bar bind:status={enrichment} />
	<button
		on:click={() => {
			web3Props.contract.play();
		}}>Play</button
	>
</div>
<div>
	Happiness: {happiness}
	<Bar bind:status={happiness} />
</div>
<div>
	🪦: {tombstones}
</div>

<style>
	div {
		width: 33%;
	}
</style>
