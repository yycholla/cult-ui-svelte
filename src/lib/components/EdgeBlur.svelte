<script lang="ts">
	import { cn } from '$lib/utils/cn';
	let { class: className = '', position = 'bottom', size = 'h-24' }: { class?: string; position?: 'top' | 'bottom' | 'left' | 'right'; size?: string } = $props();
	const pos = { top: 'inset-x-0 top-0 bg-gradient-to-b', bottom: 'inset-x-0 bottom-0 bg-gradient-to-t', left: 'inset-y-0 left-0 bg-gradient-to-r w-24', right: 'inset-y-0 right-0 bg-gradient-to-l w-24' } as const;
</script>

<div class={cn('pointer-events-none absolute z-10 from-background via-background/80 to-transparent backdrop-blur-[2px]', position === 'left' || position === 'right' ? '' : size, pos[position], className)}></div>
