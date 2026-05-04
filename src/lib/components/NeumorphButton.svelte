<script lang="ts">
	import type { Snippet } from 'svelte';
	import type { HTMLButtonAttributes } from 'svelte/elements';
	import { cn } from '$lib/utils/cn';

	type Intent = 'default' | 'primary' | 'secondary' | 'danger';
	type Size = 'small' | 'medium' | 'large';

	let {
		class: className = '',
		children,
		intent = 'default',
		size = 'medium',
		fullWidth = false,
		loading = false,
		disabled = false,
		...rest
	}: {
		class?: string;
		children?: Snippet;
		intent?: Intent;
		size?: Size;
		fullWidth?: boolean;
		loading?: boolean;
	} & HTMLButtonAttributes = $props();

	const intents: Record<Intent, string> = {
		default: 'bg-[#36322F] text-white hover:enabled:bg-[#4a4542] disabled:bg-[#8c8885] [box-shadow:inset_0px_-2.108px_0px_0px_#171310,_0px_1.204px_6.325px_0px_rgba(58,33,8,58%)] hover:enabled:[box-shadow:inset_0px_-2.53px_0px_0px_#171310,_0px_1.44px_7.59px_0px_rgba(58,33,8,64%)] active:bg-[#2A2724] active:[box-shadow:inset_0px_-1.5px_0px_0px_#171310,_0px_0.5px_2px_0px_rgba(58,33,8,70%)]',
		primary: 'bg-[#2C7BE5] text-white hover:enabled:bg-[#3D8DF5] disabled:bg-[#9FC3F5] [box-shadow:inset_0px_-2.108px_0px_0px_#1A68D1,_0px_1.204px_6.325px_0px_rgba(28,100,242,58%)] hover:enabled:[box-shadow:inset_0px_-2.53px_0px_0px_#2C7BE5,_0px_1.44px_7.59px_0px_rgba(28,100,242,64%)] active:bg-[#1A68D1]',
		secondary: 'bg-white text-[#36322F] hover:enabled:bg-[#F8F8F8] disabled:bg-[#F0F0F0] border border-[#E0E0E0] [box-shadow:inset_0px_-2.108px_0px_0px_#E0E0E0,_0px_1.204px_6.325px_0px_rgba(0,0,0,10%)] active:bg-[#F0F0F0]',
		danger: 'bg-[#E6492D] text-white hover:enabled:bg-[#F05B41] disabled:bg-[#F5A799] [box-shadow:inset_0px_-2.108px_0px_0px_#D63A1F,_0px_1.204px_6.325px_0px_rgba(214,58,31,58%)] active:bg-[#D63A1F]'
	};
	const sizes: Record<Size, string> = { small: 'text-xs py-1 px-2 h-9 rounded-[8px]', medium: 'text-base py-2 px-4 h-11 rounded-[9px] uppercase', large: 'text-lg py-3 px-6 h-14 rounded-[11px]' };
</script>

<button
	class={cn('inline-flex items-center justify-center px-4 text-sm font-medium transition-[box-shadow,background-color,transform] disabled:cursor-not-allowed disabled:opacity-50 active:scale-[0.98] hover:enabled:scale-[1.02]', intents[intent], sizes[size], fullWidth && 'w-full', className)}
	disabled={disabled || loading}
	{...rest}
>
	{#if loading}
		<span class="mr-2 h-4 w-4 animate-spin rounded-full border-2 border-current border-t-transparent" aria-hidden="true"></span>
	{/if}
	<span class={cn('transition-opacity duration-200', loading && 'opacity-70')}>
		{@render children?.()}
	</span>
</button>
