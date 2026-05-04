<script lang="ts">
	import { cn } from '$lib/utils/cn';
	import type { Snippet } from 'svelte';

	let {
		class: className = '',
		children,
	}: {
		class?: string;
		children?: Snippet;
	} = $props();
</script>

<figure
	class={cn('inline-flex flex-col gap-3', className)}
	data-slot="dither-image"
>
	{@render children?.()}
</figure>
