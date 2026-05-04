<script lang="ts">
	import type { Snippet } from 'svelte';
	import { cn } from '$lib/utils/cn';
	let { class: className = '', children, label = 'New' }: { class?: string; children?: Snippet; label?: string } = $props();
</script>

<span class={cn('inline-flex items-center rounded-full bg-[#f4f1ed] px-3 py-1 text-xs font-semibold uppercase tracking-[0.18em] text-[#36322f] shadow-[inset_0_1px_0_rgba(255,255,255,0.8),inset_0_-1px_1px_rgba(0,0,0,0.08),0_1px_3px_rgba(0,0,0,0.08)] dark:bg-neutral-900 dark:text-neutral-200 dark:shadow-[inset_0_1px_0_rgba(255,255,255,0.06),inset_0_-1px_1px_rgba(0,0,0,0.5),0_1px_3px_rgba(0,0,0,0.3)]', className)}>
	{#if children}{@render children()}{:else}{label}{/if}
</span>
