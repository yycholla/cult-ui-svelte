<script lang="ts">
	import { cn } from '$lib/utils/cn';
	let { class: className = '', direction = 'right' }: { class?: string; direction?: 'right' | 'left' | 'up' | 'down' } = $props();
	const rotate = { right: '', left: 'rotate-180', up: '-rotate-90', down: 'rotate-90' } as const;
</script>

<svg class={cn('h-12 w-24 overflow-visible text-current', rotate[direction], className)} viewBox="0 0 120 60" fill="none" aria-hidden="true">
	<path d="M4 36 C 18 12, 35 12, 48 34 S 77 56, 96 24" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round" />
	<path d="M92 12 L108 22 L94 36" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round" />
</svg>
