<script lang="ts">
	import { cn } from '$lib/utils/cn';
	type Item = { id: string; label: string; icon: 'grid' | 'chart' | 'layers' | 'storage' };
	let { class: className = '', items = [ { id: 'dashboard', label: 'Dashboard', icon: 'grid' }, { id: 'analytics', label: 'Analytics', icon: 'chart' }, { id: 'layers', label: 'Layers', icon: 'layers' }, { id: 'storage', label: 'Storage', icon: 'storage' } ], active = 'dashboard', dark = true }: { class?: string; items?: Item[]; active?: string; dark?: boolean } = $props();
</script>

<div class={cn('flex w-full justify-center py-1', className)}>
	<div class={cn('relative inline-flex items-center rounded-[28px] p-1 shadow-inner transition-colors', dark ? 'bg-[#111113] text-white' : 'bg-[#d1d1d6] text-zinc-900')}>
		<div class="relative z-10 flex gap-1 rounded-[24px] border border-black/10 bg-white/80 p-1 shadow-[0_8px_30px_rgba(0,0,0,0.12)] dark:border-white/5 dark:bg-[#141416]">
			{#each items as item (item.id)}
				<button
					type="button"
					class={cn('relative flex items-center gap-2 rounded-[18px] px-3 py-2 text-sm font-medium transition-all duration-200', active === item.id ? 'text-current' : dark ? 'text-zinc-500 hover:text-zinc-300' : 'text-zinc-400 hover:text-zinc-700')}
					onclick={() => (active = item.id)}
				>
					{#if active === item.id}
						<span class={cn('absolute inset-0 rounded-[18px] border shadow-sm transition-all', dark ? 'border-white/10 bg-gradient-to-b from-[#1f1f22] to-[#101012]' : 'border-black/10 bg-gradient-to-b from-white to-[#f0f0f2]')}></span>
					{/if}
					<span class="relative z-10 size-5">
						{#if item.icon === 'grid'}<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="3" y="3" width="7" height="7" rx="1"/><rect x="14" y="3" width="7" height="7" rx="1"/><rect x="3" y="14" width="7" height="7" rx="1"/><rect x="14" y="14" width="7" height="7" rx="1"/></svg>{/if}
						{#if item.icon === 'chart'}<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><line x1="8" y1="17" x2="8" y2="11"/><line x1="12" y1="17" x2="12" y2="7"/><line x1="16" y1="17" x2="16" y2="13"/></svg>{/if}
						{#if item.icon === 'layers'}<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M12 2L2 7l10 5 10-5-10-5z"/><path d="M2 17l10 5 10-5"/><path d="M2 12l10 5 10-5"/></svg>{/if}
						{#if item.icon === 'storage'}<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M4 4h16v6H4z"/><path d="M4 14h16v6H4z"/><circle cx="7" cy="7" r="1" fill="currentColor"/><circle cx="7" cy="17" r="1" fill="currentColor"/></svg>{/if}
					</span>
					<span class="relative z-10 hidden sm:inline">{item.label}</span>
				</button>
			{/each}
		</div>
		<button type="button" class={cn('ml-1 rounded-full p-3 transition', dark ? 'text-zinc-300 hover:bg-white/5' : 'text-zinc-700 hover:bg-black/5')} onclick={() => (dark = !dark)} aria-label="Toggle group theme">
			{#if dark}☾{:else}☼{/if}
		</button>
	</div>
</div>
