<script lang="ts">
	import { cn } from '$lib/utils/cn';
	import { setContext } from 'svelte';
	import type { Snippet } from 'svelte';

	type DitherSize = 'xs' | 'sm' | 'md' | 'lg' | 'xl' | '2xl';
	type DitherAspectRatio =
		| 'square'
		| 'video'
		| 'portrait'
		| 'wide'
		| (string & {})
		| number;

	const DITHER_SIZE_CLASS: Record<DitherSize, string> = {
		xs: 'dither-xs',
		sm: 'dither-sm',
		md: 'dither-md',
		lg: 'dither-lg',
		xl: 'dither-xl',
		'2xl': 'dither-2xl',
	};

	function resolveAspectRatio(ratio: DitherAspectRatio): string {
		if (typeof ratio === 'number') return String(ratio);
		if (ratio === 'square') return '1 / 1';
		if (ratio === 'video') return '16 / 9';
		if (ratio === 'portrait') return '3 / 4';
		if (ratio === 'wide') return '21 / 9';
		return ratio;
	}

	let {
		class: className = '',
		children,
		size = 'lg',
		aspectRatio,
		grayscale,
		contrast,
		brightness,
		blur,
		opacity,
		rounded = true,
		invertOnDark = false,
		style = '',
	}: {
		class?: string;
		children?: Snippet;
		size?: DitherSize;
		aspectRatio?: DitherAspectRatio;
		grayscale?: number;
		contrast?: number;
		brightness?: number;
		blur?: number | string;
		opacity?: number;
		rounded?: boolean | string;
		invertOnDark?: boolean;
		style?: string;
	} = $props();

	const cssVars = $derived.by((): string => {
		const parts: string[] = [];
		if (grayscale !== undefined) parts.push(`--dither-gray:${grayscale}`);
		if (contrast !== undefined) parts.push(`--dither-contrast:${contrast}`);
		if (brightness !== undefined) parts.push(`--dither-bright:${brightness}`);
		if (blur !== undefined) {
			parts.push(
				`--dither-blur:${typeof blur === 'number' ? `${blur}px` : blur}`
			);
		}
		if (opacity !== undefined) parts.push(`--dither-opacity:${opacity}`);
		if (aspectRatio !== undefined) {
			parts.push(`aspect-ratio:${resolveAspectRatio(aspectRatio)}`);
		}
		return parts.join(';') + (style ? `;${style}` : '');
	});

	const roundedClass = $derived.by((): string | undefined => {
		if (rounded === true) return 'rounded-xl';
		if (typeof rounded === 'string') return rounded;
		return undefined;
	});

	setContext('dither-image-frame', {
		get invertOnDark() {
			return invertOnDark;
		}
	});
</script>

{#if invertOnDark}
	<div class="dark:invert">
		<div
			class={cn(
				DITHER_SIZE_CLASS[size],
				'relative block w-full',
				roundedClass,
				className
			)}
			data-size={size}
			data-slot="dither-image-frame"
			style={cssVars}
		>
			{@render children?.()}
		</div>
	</div>
{:else}
	<div
		class={cn(
			DITHER_SIZE_CLASS[size],
			'relative block w-full',
			roundedClass,
			className
		)}
		data-size={size}
		data-slot="dither-image-frame"
		style={cssVars}
	>
		{@render children?.()}
	</div>
{/if}
