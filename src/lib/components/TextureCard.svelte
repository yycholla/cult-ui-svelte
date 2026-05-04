<script lang="ts">
	import type { Snippet } from 'svelte';
	import { cn } from '$lib/utils/cn';
	let { class: className = '', children, title = 'Texture Card', description = 'Subtle border, grain, and soft gradient surface.' }: { class?: string; children?: Snippet; title?: string; description?: string } = $props();
</script>

<div class={cn('relative overflow-hidden rounded-2xl border border-black/10 bg-gradient-to-b from-white to-neutral-100 p-6 shadow-sm dark:border-white/10 dark:from-neutral-900 dark:to-neutral-950', className)}>
	<div class="pointer-events-none absolute inset-0 opacity-[0.07] [background-image:radial-gradient(currentColor_1px,transparent_1px)] [background-size:8px_8px]"></div>
	<div class="pointer-events-none absolute inset-x-0 top-0 h-px bg-gradient-to-r from-transparent via-white/80 to-transparent"></div>
	<div class="relative">
		{#if children}
			{@render children()}
		{:else}
			<h3 class="text-lg font-semibold text-neutral-950 dark:text-white">{title}</h3>
			<p class="mt-2 text-sm text-neutral-500 dark:text-neutral-400">{description}</p>
		{/if}
	</div>
</div>
