<script lang="ts">
	import { cn } from '$lib/utils/cn';
	import { getContext } from 'svelte';

	const ctx = getContext<{ invertOnDark: boolean } | null>(
		'dither-image-frame'
	);

	let {
		class: className = '',
		src,
		alt,
		...imgProps
	}: {
		class?: string;
		src: string;
		alt: string;
		[key: string]: unknown;
	} = $props();

	const counterInvert = $derived(ctx?.invertOnDark ? 'dark:invert' : undefined);
</script>

<img
	{src}
	{alt}
	class={cn(
		'block h-full w-full object-cover',
		counterInvert,
		className
	)}
	data-slot="dither-image-content"
	{...imgProps}
/>
