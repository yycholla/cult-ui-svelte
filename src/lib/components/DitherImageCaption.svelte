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

<!-- svelte-ignore a11y_figcaption_parent -->
<figcaption
	class={cn(
		'text-pretty text-muted-foreground text-sm leading-relaxed',
		className
	)}
	data-slot="dither-image-caption"
>
	{@render children?.()}
</figcaption>
