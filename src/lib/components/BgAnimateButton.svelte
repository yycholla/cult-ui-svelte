<script lang="ts">
	import type { Snippet } from 'svelte';
	import type { HTMLButtonAttributes } from 'svelte/elements';
	import { cn } from '$lib/utils/cn';
	type Size = 'sm' | 'default' | 'lg';
	type Rounded = 'full' | 'xl' | '2xl' | '3xl' | 'sm' | 'xs' | 'base';
	type Shadow = 'flat' | 'soft' | 'base' | 'deep' | 'deeper';
	type Gradient = 'sunrise' | 'ocean' | 'candy' | 'default' | 'forest' | 'sunset' | 'nebula';
	type Animation = 'spin' | 'pulse' | 'spin-slow' | 'spin-fast';
	let { class: className = '', children, size = 'default', rounded = 'full', shadow = 'soft', gradient = 'forest', animation = 'spin', ...rest }: { class?: string; children?: Snippet; size?: Size; rounded?: Rounded; shadow?: Shadow; gradient?: Gradient; animation?: Animation } & HTMLButtonAttributes = $props();
	const roundedClass: Record<Rounded,string> = { full:'rounded-full', xl:'rounded-xl', '2xl':'rounded-2xl', '3xl':'rounded-3xl', sm:'rounded-sm', xs:'rounded-xs', base:'rounded' };
	const sizeClass: Record<Size,string> = { sm:'text-xs px-4 py-1', default:'text-sm px-6 py-2', lg:'text-base px-8 py-3' };
	const shadowClass: Record<Shadow,string> = { flat:'', soft:'shadow-[0_2px_4px_rgba(0,0,0,0.15),inset_0_1px_1px_rgba(255,255,255,0.15),inset_0_-1px_2px_rgba(0,0,0,0.3)]', base:'shadow-[0_3px_5px_rgba(0,0,0,0.2),inset_0_0.5px_1px_rgba(255,255,255,0.1),inset_0_-2px_3px_rgba(0,0,0,0.4)]', deep:'shadow-[0_4px_6px_rgba(0,0,0,0.25),inset_0_1px_2px_rgba(255,255,255,0.2),inset_0_-2px_4px_rgba(0,0,0,0.5)]', deeper:'shadow-[0_6px_8px_rgba(0,0,0,0.3),inset_0_2px_3px_rgba(255,255,255,0.25),inset_0_-3px_6px_rgba(0,0,0,0.6)]' };
	const gradientClass: Record<Gradient,string> = { sunrise:'bg-[conic-gradient(from_90deg_at_50%_50%,#ffecd2_0%,#fcb69f_50%,#ffecd2_100%)]', ocean:'bg-[conic-gradient(from_90deg_at_50%_50%,#a1c4fd_0%,#c2e9fb_50%,#a1c4fd_100%)]', candy:'bg-[conic-gradient(from_90deg_at_50%_50%,#ff9a9e_0%,#fad0c4_50%,#ff9a9e_100%)]', forest:'bg-[conic-gradient(from_90deg_at_50%_50%,#85d797_0%,#1a806b_50%,#85d797_100%)]', sunset:'bg-[conic-gradient(from_90deg_at_50%_50%,#fe5d75_0%,#f5af19_50%,#fe5d75_100%)]', nebula:'bg-[conic-gradient(from_90deg_at_50%_50%,#A77BFE_0%,#8860D0_50%,#A77BFE_100%)]', default:'bg-[conic-gradient(from_90deg_at_50%_50%,#E2CBFF_0%,#393BB2_50%,#E2CBFF_100%)]' };
	const animationClass: Record<Animation,string> = { spin:'animate-[spin_4s_linear_infinite]', pulse:'animate-pulse', 'spin-slow':'animate-[spin_8s_linear_infinite]', 'spin-fast':'animate-[spin_2s_linear_infinite]' };
</script>

<button class={cn('relative inline-block overflow-hidden p-[2px] disabled:pointer-events-none disabled:opacity-50', roundedClass[rounded], className)} {...rest}>
	<span class={cn('absolute inset-[-1000%] m-auto block', gradientClass[gradient], animationClass[animation])}></span>
	<span class={cn('relative flex items-center justify-center overflow-hidden bg-background text-foreground transition-all duration-150 ease-in-out', sizeClass[size], shadowClass[shadow], roundedClass[rounded])}>
		{@render children?.()}
	</span>
</button>
