<script lang="ts">
	import type { Snippet } from 'svelte';
	import { cn } from '$lib/utils/cn';
	let { class: className = '', children, title = 'Cutout Card', description = 'Layered paper texture with clipped corners.' }: { class?: string; children?: Snippet; title?: string; description?: string } = $props();
</script>

<div class={cn('relative overflow-hidden rounded-3xl border border-black/10 bg-neutral-100 p-1 shadow-sm dark:border-white/10 dark:bg-neutral-900', className)}>
	<div class="pointer-events-none absolute -right-12 -top-12 size-32 rounded-full bg-background shadow-[0_0_0_999px_rgba(0,0,0,0.03)] dark:shadow-[0_0_0_999px_rgba(255,255,255,0.03)]"></div>
	<div class="relative rounded-[1.35rem] border border-black/5 bg-white p-6 dark:border-white/10 dark:bg-neutral-950">
		<div class="absolute right-3 top-3 size-10 rounded-bl-3xl bg-neutral-100 dark:bg-neutral-900"></div>
		{#if children}
			{@render children()}
		{:else}
			<h3 class="text-lg font-semibold text-neutral-950 dark:text-white">{title}</h3>
			<p class="mt-2 max-w-sm text-sm text-neutral-500 dark:text-neutral-400">{description}</p>
		{/if}
	</div>
</div>
