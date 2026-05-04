<script lang="ts">
	import type { Snippet } from 'svelte';
	import type { HTMLButtonAttributes } from 'svelte/elements';
	import { cn } from '$lib/utils/cn';
	let { class: className = '', borderBeamClass = '', children, duration = 3, active = true, ...rest }: { class?: string; borderBeamClass?: string; children?: Snippet; duration?: number; active?: boolean } & HTMLButtonAttributes = $props();
</script>

<span class={cn('relative inline-flex w-fit overflow-hidden rounded-xl p-[1px]', borderBeamClass)}>
	{#if active}
		<span class="absolute inset-[-200%] bg-[conic-gradient(from_0deg,transparent_0deg,#60a5fa_70deg,#c084fc_130deg,transparent_190deg,transparent_360deg)] opacity-90" style={`animation: spin ${duration}s linear infinite`}></span>
	{/if}
	<button class={cn('relative inline-flex items-center justify-center rounded-[11px] bg-background px-4 py-2 text-sm font-medium text-foreground shadow-sm transition hover:bg-muted disabled:pointer-events-none disabled:opacity-50', className)} {...rest}>
		{@render children?.()}
	</button>
</span>
