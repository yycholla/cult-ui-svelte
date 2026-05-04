<script lang="ts">
	import { cn } from '$lib/utils/cn';
	import type { Snippet } from 'svelte';

	const NUMERIC_SIZE_RE = /^\d+$/;

	let {
		class: className = '',
		children,
		size,
	}: {
		class?: string;
		children?: Snippet;
		size?: number | string;
	} = $props();

	const sizeClass = $derived.by((): string | undefined => {
		if (size === undefined) return undefined;
		if (typeof size === 'number') return `size-${size}`;
		if (NUMERIC_SIZE_RE.test(size)) return `size-${size}`;
		return size;
	});
</script>

<div
	class={cn('relative overflow-hidden', sizeClass, className)}
	data-slot="dither-image-reveal"
>
	{@render children?.()}
</div>
