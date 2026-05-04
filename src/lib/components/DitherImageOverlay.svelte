<script lang="ts">
	import { cn } from '$lib/utils/cn';

	type DitherRevealDirection =
		| 'l'
		| 'r'
		| 't'
		| 'b'
		| 'tl-br'
		| 'tr-bl'
		| 'bl-tr'
		| 'br-tl'
		| 'radial';

	function revealMaskImage(
		direction: DitherRevealDirection,
		from: number,
		to: number
	): string {
		const a = Math.min(from, to);
		const b = Math.max(from, to);
		switch (direction) {
			case 'r':
				return `linear-gradient(to right, black ${a}%, transparent ${b}%)`;
			case 'l':
				return `linear-gradient(to left, black ${a}%, transparent ${b}%)`;
			case 't':
				return `linear-gradient(to bottom, black ${a}%, transparent ${b}%)`;
			case 'b':
				return `linear-gradient(to top, black ${a}%, transparent ${b}%)`;
			case 'tl-br':
				return `linear-gradient(to bottom right, black ${a}%, transparent ${b}%)`;
			case 'tr-bl':
				return `linear-gradient(to bottom left, black ${a}%, transparent ${b}%)`;
			case 'bl-tr':
				return `linear-gradient(to top right, black ${a}%, transparent ${b}%)`;
			case 'br-tl':
				return `linear-gradient(to top left, black ${a}%, transparent ${b}%)`;
			case 'radial':
				return `radial-gradient(circle at center, black ${a}%, transparent ${b}%)`;
		}
	}

	function revealMaskStyle(
		direction: DitherRevealDirection,
		from: number,
		to: number
	): string {
		const img = revealMaskImage(direction, from, to);
		return [
			`-webkit-mask-image:${img}`,
			`mask-image:${img}`,
			'-webkit-mask-size:100% 100%',
			'mask-size:100% 100%',
			'-webkit-mask-repeat:no-repeat',
			'mask-repeat:no-repeat',
		].join(';');
	}

	let {
		class: className = '',
		src,
		alt,
		direction = 'r',
		from = 0,
		to = 65,
		maskClassName,
		style = '',
		...rest
	}: {
		class?: string;
		src: string;
		alt: string;
		direction?: DitherRevealDirection;
		from?: number;
		to?: number;
		maskClassName?: string;
		style?: string;
		[key: string]: unknown;
	} = $props();

	const typedMaskStyle = $derived(
		maskClassName === undefined ? revealMaskStyle(direction, from, to) : ''
	);
</script>

<img
	{src}
	{alt}
	class={cn(
		'pointer-events-none absolute inset-0 h-full w-full object-cover',
		maskClassName === undefined && 'mask',
		maskClassName,
		className
	)}
	data-slot="dither-image-overlay"
	style={typedMaskStyle ? `${typedMaskStyle};${style}` : style}
	{...rest}
/>
