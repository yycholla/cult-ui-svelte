<script lang="ts">
	import type { Snippet } from 'svelte';
	import type { HTMLButtonAttributes } from 'svelte/elements';
	import { cn } from '$lib/utils/cn';

	type Variant = 'primary' | 'secondary' | 'accent' | 'destructive' | 'minimal' | 'icon';
	type Size = 'sm' | 'default' | 'lg' | 'icon';

	let {
		class: className = '',
		children,
		variant = 'primary',
		size = 'default',
		...rest
	}: {
		class?: string;
		children?: Snippet;
		variant?: Variant;
		size?: Size;
	} & HTMLButtonAttributes = $props();

	const outer: Record<Variant, string> = {
		primary: 'w-full border border-black/10 dark:border-2 dark:border-black bg-gradient-to-b from-black/70 to-black dark:from-white dark:to-white/80 p-[1px] transition duration-300 ease-in-out',
		accent: 'w-full border border-black/10 dark:border-2 dark:border-neutral-950 bg-gradient-to-b from-indigo-300/90 to-indigo-500 dark:from-indigo-200/70 dark:to-indigo-500 p-[1px] transition duration-300 ease-in-out',
		destructive: 'w-full border border-black/10 dark:border-2 dark:border-neutral-950 bg-gradient-to-b from-red-300/90 to-red-500 p-[1px] transition duration-300 ease-in-out',
		secondary: 'w-full border border-black/20 dark:border-2 dark:border-neutral-950 bg-white/50 dark:bg-neutral-600/50 p-[1px] transition duration-300 ease-in-out',
		minimal: 'group/texture-button w-full border border-black/20 dark:border-2 dark:border-neutral-950 bg-white/50 dark:bg-neutral-600/80 p-[1px] active:bg-neutral-200 dark:active:bg-neutral-800 hover:bg-gradient-to-t hover:from-neutral-100 hover:to-white dark:hover:from-neutral-600/50 dark:hover:to-neutral-600/70',
		icon: 'group/texture-button rounded-full border border-black/10 dark:border-neutral-950 bg-white/50 dark:bg-neutral-600/50 p-[1px] active:bg-neutral-200 dark:active:bg-neutral-800 hover:bg-gradient-to-t hover:from-neutral-100 hover:to-white dark:hover:from-neutral-700 dark:hover:to-neutral-600'
	};
	const inner: Record<Variant, string> = {
		primary: 'gap-2 bg-gradient-to-b from-neutral-800 to-black dark:from-neutral-200 dark:to-neutral-50 text-sm text-white/90 dark:text-black/80 transition duration-300 ease-in-out hover:from-stone-800 hover:to-neutral-800/70 dark:hover:from-stone-200 dark:hover:to-neutral-200 active:from-black active:to-black',
		accent: 'gap-2 bg-gradient-to-b from-indigo-400 to-indigo-600 text-sm text-white/90 transition duration-300 ease-in-out hover:from-indigo-400/70 hover:to-indigo-600/70 active:from-indigo-400/80 active:to-indigo-600/80',
		destructive: 'gap-2 bg-gradient-to-b from-red-400/60 to-red-500/60 text-sm text-white/90 transition duration-300 ease-in-out hover:from-red-400/70 hover:to-red-600/70 active:from-red-400/80 active:to-red-600/80',
		secondary: 'bg-gradient-to-b from-neutral-100/80 to-neutral-200/50 dark:from-neutral-800 dark:to-neutral-700/50 text-sm transition duration-300 ease-in-out hover:from-neutral-200/40 hover:to-neutral-300/60 dark:hover:from-neutral-700 dark:hover:to-neutral-700/60 active:from-neutral-200/60 active:to-neutral-300/70',
		minimal: 'bg-gradient-to-b from-white to-neutral-50/50 dark:from-neutral-800 dark:to-neutral-700/50 text-sm transition duration-300 ease-in-out group-hover/texture-button:from-neutral-50/50 group-hover/texture-button:to-neutral-100/60 dark:group-hover/texture-button:from-neutral-700 dark:group-hover/texture-button:to-neutral-700/60',
		icon: 'bg-gradient-to-b from-white to-neutral-50/50 dark:from-neutral-800 dark:to-neutral-700/50 rounded-full group-active/texture-button:bg-neutral-200 dark:group-active/texture-button:bg-neutral-800'
	};
	const outerSize: Record<Size, string> = { sm: 'rounded-[6px]', default: 'rounded-[12px]', lg: 'rounded-[12px]', icon: 'rounded-full' };
	const innerSize: Record<Size, string> = { sm: 'text-xs rounded-[4px] px-4 py-1', default: 'text-sm rounded-[10px] px-4 py-2', lg: 'text-base rounded-[10px] px-4 py-2', icon: 'rounded-full p-1' };
</script>

<button class={cn(outer[variant], outerSize[size], className)} {...rest}>
	<span class={cn('flex h-full w-full items-center justify-center text-muted-foreground', inner[variant], innerSize[size])}>
		{@render children?.()}
	</span>
</button>
