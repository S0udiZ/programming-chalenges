<script lang="ts">
	import { LightSwitch } from '@skeletonlabs/skeleton';

	import { writable } from 'svelte/store';

	const coin = writable('heads');
	const duration = writable(1000);
	const disabled = writable(false);

	function flipCoin(e:Event) {
		e.target.disabled = true;
		$duration = (Math.random() * 1501) + 1500;
		$coin = 'spinning';
		const flippedCoin = Math.random() > 0.5 ? 'heads' : 'tails';
		setTimeout(() => {
			$coin = flippedCoin;
		}, $duration);
		setTimeout(() => {
			e.target.disabled = false;
		}, $duration);
	}

	import spinningCoin from '../assets/svg/heads-or-tails-456.svg';
</script>

<LightSwitch class="fixed top-5 right-16" />
<div class="container h-full mx-auto flex flex-wrap justify-center items-center">
	<div class="space-y-4 text-center border-4 border-accent-500 rounded-xl p-10">
		<figure class="w-64">
			{#if $coin === 'spinning'}
				<img class="spinning-coin" src={spinningCoin} alt="Spinning coin" />
			{:else if $coin === 'heads'}
				<img src="https://www.royalmint.com/globalassets/the-royal-mint/images/pages/new-pound-coin/large_new_pound.png" alt="Heads" />
			{:else}
				<img src="https://www.royalmint.com/globalassets/the-royal-mint/images/pages/new-pound-coin/large_new_pound_rev.png" alt="Tails" />
			{/if}
		</figure>
		<h2>{$coin.toUpperCase()}</h2>
		<button class="border-4 bg-accent-500 rounded-full p-2 px-8" on:click={flipCoin} disabled={$disabled}>Flip a coin</button>
	</div>
</div>

<style>
	.spinning-coin {
		animation: spin 500ms linear infinite;
	}

	@keyframes spin {
		0% {
			transform: rotate(0deg);
		}
		100% {
			transform: rotate(360deg);
		}
	}
</style>