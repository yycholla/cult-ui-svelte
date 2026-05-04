<script lang="ts">
	import type { Snippet } from 'svelte';
	import type { HTMLButtonAttributes } from 'svelte/elements';
	import BorderBeamButton from './BorderBeamButton.svelte';
	import { cn } from '$lib/utils/cn';
	let { class: className = '', children, ...rest }: { class?: string; children?: Snippet } & HTMLButtonAttributes = $props();
</script>

<BorderBeamButton class={cn('size-9 px-0 [&_svg]:block [&_svg]:size-4 [&_svg]:shrink-0', className)} {...rest}>
	{@render children?.()}
</BorderBeamButton>
