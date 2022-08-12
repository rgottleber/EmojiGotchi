<script>
	import Bar from './Bar.svelte';
	import Face from './Face.svelte';
	import { ethers } from 'ethers';
	import EmojiGotchiAbi from '../contracts/EmojiGotchi.json';
	export let contractAddr;
	export let url;

	$: image = '';
	$: hunger = '';
	$: enrichment = '';
	$: happiness = '';
	$: tombstones = '';
	const getMyGotchi = async () => {
		var provider = new ethers.providers.JsonRpcProvider(url);
		const contract = new ethers.Contract(contractAddr, EmojiGotchiAbi.abi, provider);
		let currentGotchi = await contract.myGotchi();

		image = await currentGotchi[5];
		happiness = await currentGotchi[0].toNumber();
		hunger = await currentGotchi[1].toNumber();
		enrichment = await currentGotchi[2].toNumber();
		tombstones = await currentGotchi[3].toNumber();
		//check again after 1 minute
		setTimeout(getMyGotchi, 60000);
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
</div>
<div>
	Enrichment: {enrichment}
	<br />

	<Bar bind:status={enrichment} />
</div>
<div>
	Happiness: {happiness}
	<Bar bind:status={happiness} />
</div>
<div class="text-4xl">
	🪦: {tombstones}
</div>

<style>
	div {
		width: 33%;
	}
</style>
