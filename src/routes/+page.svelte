<script lang="ts">
	import Checkbox from '$lib/components/Checkbox.svelte';
	let selectedValues: [] = $state([]);

	const options = [
		{ label: 'Marketing', value: 'marketing' },
		{ label: 'Promotions', value: 'promotions' },
		{ label: 'News', value: 'news' },
		{ label: 'Special Offers', value: 'special' }
	];
</script>

<h1>Welcome to Flipopay</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p>

<Checkbox name="notifications" {options} bind:value={selectedValues} disabled={true} />

<Checkbox name="notifications" {options} bind:value={selectedValues} />
