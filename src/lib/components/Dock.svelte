<script lang="ts">
	import { setContext } from 'svelte';
	import { cn } from '$lib/utils/cn';

	interface DockContext {
		get mouseX(): number;
		get hovered(): boolean;
		get animatingIndexes(): number[];
		setAnimatingIndexes(indexes: number[]): void;
	}

	let {
		class: className = '',
		children,
	}: {
		class?: string;
		children?: import('svelte').Snippet;
	} = $props();

	let dockEl = $state<HTMLDivElement>();
	let hovered = $state(false);
	let mouseX = $state(Infinity);
	let animatingIndexes = $state<number[]>([]);

	function setAnimatingIndexes(indexes: number[]) {
		animatingIndexes = indexes;
	}

	function handleMouseMove(e: MouseEvent) {
		mouseX = e.pageX;
		if (!hovered) hovered = true;
	}

	function handleMouseLeave() {
		mouseX = Infinity;
		hovered = false;
	}

	setContext<DockContext>('dock', {
		get mouseX() {
			return mouseX;
		},
		get hovered() {
			return hovered;
		},
		get animatingIndexes() {
			return animatingIndexes;
		},
		setAnimatingIndexes,
	});
</script>

<div
	bind:this={dockEl}
	role="group"
	class={cn(
		'absolute bottom-4 left-1/2 -translate-x-1/2 flex items-end h-14 p-2 gap-3 rounded-xl bg-opacity-90',
		'dark:bg-neutral-900 bg-neutral-50 shadow-sm transition-colors hover:bg-neutral-100 dark:hover:bg-neutral-800/80',
		'shadow-[0px_1px_1px_0px_rgba(0,0,0,0.05),0px_1px_1px_0px_rgba(255,252,240,0.5)_inset,0px_0px_0px_1px_hsla(0,0%,100%,0.1)_inset,0px_0px_1px_0px_rgba(28,27,26,0.5)]',
		'shadow-[rgba(17,24,28,0.08)_0_0_0_1px,rgba(17,24,28,0.08)_0_1px_2px_-1px,rgba(17,24,28,0.04)_0_2px_4px]',
		'dark:shadow-[0_1px_0_0_rgba(255,255,255,0.03)_inset,0_0_0_1px_rgba(255,255,255,0.03)_inset,0_0_0_1px_rgba(0,0,0,0.1),0_2px_2px_0_rgba(0,0,0,0.1),0_4px_4px_0_rgba(0,0,0,0.1),0_8px_8px_0_rgba(0,0,0,0.1)]',
		className
	)}
	onmousemove={handleMouseMove}
	onmouseleave={handleMouseLeave}
>
	{#if children}
		{@render children()}
	{/if}
</div>
