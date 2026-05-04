<script lang="ts">
	import { cn } from '$lib/utils/cn';

	let {
		class: className = '',
		children,
	}: {
		class?: string;
		children?: import('svelte').Snippet;
	} = $props();
</script>

<p class={cn('text-sm text-neutral-500 pb-2 px-1', className)}>
	{@render children?.()}
</p>
