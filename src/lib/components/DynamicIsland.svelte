<script lang="ts">
	import { onMount } from 'svelte';
	import type { Snippet } from 'svelte';
	import { cn } from '$lib/utils/cn';

	const MIN_WIDTH = 691;
	const MAX_HEIGHT_MOBILE_ULTRA = 400;
	const MAX_HEIGHT_MOBILE_MASSIVE = 700;

	export type SizePreset =
		| 'reset'
		| 'empty'
		| 'default'
		| 'compact'
		| 'compactLong'
		| 'large'
		| 'long'
		| 'minimalLeading'
		| 'minimalTrailing'
		| 'compactMedium'
		| 'medium'
		| 'tall'
		| 'ultra'
		| 'massive';

	interface Preset {
		width: number;
		height?: number;
		aspectRatio: number;
		borderRadius: number;
	}

	const SIZE_PRESETS: Record<SizePreset, Preset> = {
		reset: { width: 150, aspectRatio: 1, borderRadius: 20 },
		empty: { width: 0, aspectRatio: 0, borderRadius: 0 },
		default: { width: 150, aspectRatio: 44 / 150, borderRadius: 46 },
		minimalLeading: { width: 52.33, aspectRatio: 44 / 52.33, borderRadius: 22 },
		minimalTrailing: { width: 52.33, aspectRatio: 44 / 52.33, borderRadius: 22 },
		compact: { width: 235, aspectRatio: 44 / 235, borderRadius: 46 },
		compactLong: { width: 300, aspectRatio: 44 / 235, borderRadius: 46 },
		compactMedium: { width: 351, aspectRatio: 64 / 371, borderRadius: 44 },
		long: { width: 371, aspectRatio: 84 / 371, borderRadius: 42 },
		medium: { width: 371, aspectRatio: 210 / 371, borderRadius: 22 },
		large: { width: 371, aspectRatio: 84 / 371, borderRadius: 42 },
		tall: { width: 371, aspectRatio: 210 / 371, borderRadius: 42 },
		ultra: { width: 630, aspectRatio: 630 / 800, borderRadius: 42 },
		massive: { width: 891, height: 1900, aspectRatio: 891 / 891, borderRadius: 42 }
	};

	type ScreenSize = 'mobile' | 'tablet' | 'desktop';

	let {
		preset = 'default',
		class: className,
		children,
		id
	}: {
		/** Size preset to control the island dimensions. */
		preset?: SizePreset;
		/** CSS class(es) forwarded to the root element. */
		class?: string;
		/** Content rendered inside the island. */
		children?: Snippet;
		/** Optional id attribute. */
		id?: string;
	} = $props();

	let screenSize: ScreenSize = $state('desktop');

	onMount(() => {
		const handleResize = () => {
			if (window.innerWidth <= 640) {
				screenSize = 'mobile';
			} else if (window.innerWidth <= 1024) {
				screenSize = 'tablet';
			} else {
				screenSize = 'desktop';
			}
		};

		handleResize();
		window.addEventListener('resize', handleResize);
		return () => window.removeEventListener('resize', handleResize);
	});

	const currentPreset = $derived(SIZE_PRESETS[preset]);

	const dimensions = $derived.by(() => {
		const isMassiveOnMobile = preset === 'massive' && screenSize === 'mobile';
		const isUltraOnMobile = preset === 'ultra' && screenSize === 'mobile';

		if (isMassiveOnMobile) {
			return { width: '350px', height: `${MAX_HEIGHT_MOBILE_MASSIVE}px` };
		}

		if (isUltraOnMobile) {
			return { width: '350px', height: `${MAX_HEIGHT_MOBILE_ULTRA}px` };
		}

		const width = Math.min(currentPreset.width, MIN_WIDTH);
		const height = currentPreset.aspectRatio * width;
		return { width: `${width}px`, height: `${height}px` };
	});
</script>

<div
	{id}
	class={cn(
		'mx-auto flex items-center justify-center overflow-hidden border border-black/10 bg-black text-center text-black transition-all duration-300 ease-in-out focus-within:bg-neutral-900 hover:shadow-md dark:border dark:border-white/5 dark:focus-within:bg-black',
		className
	)}
	style="width: {dimensions.width}; height: {dimensions.height}; border-radius: {currentPreset.borderRadius}px;"
>
	{#if children}
		<div class="contents">
			{@render children()}
		</div>
	{/if}
</div>
