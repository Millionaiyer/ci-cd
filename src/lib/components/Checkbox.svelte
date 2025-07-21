<script lang="ts">
	import { Checkbox } from 'bits-ui';
	import { clsx } from 'clsx';

	interface CheckboxOption {
		label: string;
		value: string;
	}

	interface Props {
		name: string;
		options: CheckboxOption[];
		value?: string[];
		class?: string;
		disabled?: boolean;
	}

	let {
		name,
		class: className,
		options,
		value = $bindable([]),
		disabled = false
	}: Props = $props();

	// Create checkbox classes using clsx
	const checkboxClasses = clsx(
		'inline-flex h-3 w-3 items-center justify-center rounded-xs border border-gray-300 bg-white data-[state=checked]:border-[#1555FC] data-[state=checked]:bg-[#1555FC]',
		{
			'!cursor-not-allowed opacity-50': disabled
		},
		className
	);
</script>

<Checkbox.Group {name} bind:value {disabled}>
	<div class="flex flex-col gap-2">
		{#each options as option}
			<div class="flex items-center space-x-2">
				<Checkbox.Root value={option.value} class={checkboxClasses} {disabled}>
					{#snippet children({ checked })}
						{#if checked}
							<svg
								width="18"
								height="18"
								viewBox="0 0 16 16"
								fill="none"
								xmlns="http://www.w3.org/2000/svg"
							>
								<rect width="16" height="16" rx="4" fill="#1555FC" />
								<path
									d="M4 8.1L6.25 10.35L12.1 4.5"
									stroke="white"
									stroke-width="1.5"
									stroke-miterlimit="10"
									stroke-linecap="round"
									stroke-linejoin="round"
								/>
							</svg>
						{/if}
					{/snippet}
				</Checkbox.Root>
				<label
					for={`${name}-${option.value}`}
					class={`text-base font-medium text-[#171717] ${disabled ? 'cursor-not-allowed text-gray-400 ' : ''}`}
				>
					{option.label}
				</label>
			</div>
		{/each}
	</div>
</Checkbox.Group>

<!-- @component
###  Props for the checkbox :

```js
interface CheckboxOption {
		label: string;
		value: string;
	}

	interface Props {
		name: string;
		options: CheckboxOption[];
		value: string[];
		class?: string;
		disabled?: boolean;
	}
```
- name:string - defines name for the checkbox
- options: CheckboxOption[] - defines options for the checkbox
- value: string[] - defines value of the checkbox
- class?: string - defines class for the checkbox
- disabled: boolean - defines disabled state

### Example on how to use : 
```js
let selectedValues: [] = $state([]);

	const options = [
		{ label: 'Marketing', value: 'marketing' },
		{ label: 'Promotions', value: 'promotions' },
		{ label: 'News', value: 'news' },
		{ label: 'Special Offers', value: 'special' }
	];

  <Group name="notifications" {options} bind:value={selectedValues} disabled={true} />
	<Group name="notifications" {options} bind:value={selectedValues} />
```
-->
