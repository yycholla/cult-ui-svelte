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

<h3 class={cn('text-lg mt-2 font-semibold leading-tight px-1', className)}>
	{@render children?.()}
</h3>
