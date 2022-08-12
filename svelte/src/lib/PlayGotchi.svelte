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
		class="my-6 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
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
		class="my-6 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
		on:click={() => {
			web3Props.contract.play();
		}}>Play</button
	>
</div>
<div>
	Happiness: {happiness}
	<Bar bind:status={happiness} />
</div>
<div class="text-4xl pb-12">
	🪦: {tombstones}
</div>

<style>
	div {
		width: 33%;
	}
</style>
