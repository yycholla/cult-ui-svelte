<script lang="ts">
	import { getContext, type Snippet } from 'svelte';
	import { cn } from '$lib/utils/cn';

	interface DockContext {
		readonly mouseX: number;
		readonly hovered: boolean;
		readonly animatingIndexes: number[];
		setAnimatingIndexes(indexes: number[]): void;
	}

	let {
		id,
		class: className = '',
		children,
	}: {
		id: number;
		class?: string;
		children?: Snippet;
	} = $props();

	const dock = getContext<DockContext>('dock');

	let itemEl = $state<HTMLButtonElement>();
	let elCenterX = $state(0);
	let isAnimating = $state(false);

	// Proximity-based scale: items grow as mouse approaches their center
	let scale = $derived.by(() => {
		if (!dock.hovered || dock.mouseX === Infinity || elCenterX === 0) return 1;
		// Use pageX from dock; compute distance from mouse to this item's center
		const distance = Math.abs(dock.mouseX - elCenterX);
		if (distance > 160) return 1;
		// Cosine curve: peaks at center, falls off smoothly
		// cos((0/160)*PI/2) = cos(0) = 1 => 1 + 0.5 = 1.5
		// cos((160/160)*PI/2) = cos(PI/2) ≈ 0 => 1 + 0 = 1
		return 1 + 0.5 * Math.cos((distance / 160) * (Math.PI / 2));
	});

	function handleClick() {
		isAnimating = !isAnimating;
		if (isAnimating) {
			dock.setAnimatingIndexes([...dock.animatingIndexes, id]);
		} else {
			dock.setAnimatingIndexes(dock.animatingIndexes.filter((i) => i !== id));
		}
	}

	// Recalculate center X on mount and on resize
	$effect(() => {
		if (!itemEl) return;
		const el = itemEl;
		function updateCenter() {
			const rect = el.getBoundingClientRect();
			// getBoundingClientRect accounts for parent transforms, but we need
			// page-relative X. The dock uses pageX, so add window.scrollX.
			elCenterX = rect.x + window.scrollX + rect.width / 2;
		}
		updateCenter();
		window.addEventListener('resize', updateCenter);
		return () => {
			window.removeEventListener('resize', updateCenter);
		};
	});
</script>

<div class="flex flex-col items-center gap-1">
	<!-- svelte-ignore a11y_no_static_element_interactions -->
	<button
		bind:this={itemEl}
		class={cn(
			'rounded-lg border aspect-square dark:border-white/5 border-black/5 border-opacity-10',
			'dark:bg-neutral-800 bg-neutral-100 saturate-90 brightness-90',
			'hover:saturate-100 hover:brightness-112',
			'active:scale-[0.95]',
			'will-change-transform',
			isAnimating && 'dock-bouncing',
			className
		)}
		style="scale: {scale}"
		onclick={handleClick}
	>
		{#if children}
			{@render children()}
		{/if}
	</button>
	{#if dock.animatingIndexes.includes(id)}
		<div class="w-1.5 h-1.5 rounded-full dark:bg-white bg-black"></div>
	{/if}
</div>

<style>
	.dock-bouncing {
		animation: dock-bounce 0.5s ease-in-out infinite;
	}

	@keyframes dock-bounce {
		0%,
		100% {
			transform: translateY(0);
		}
		50% {
			transform: translateY(-24px);
		}
	}
</style>
