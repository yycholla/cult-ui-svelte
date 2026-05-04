<script lang="ts">
	import { cn } from '$lib/utils/cn';

	let {
		src,
		alt,
		class: className = '',
	}: {
		src: string;
		alt: string;
		class?: string;
	} = $props();
</script>

<div
	class={cn(
		'relative h-[190px] w-full rounded-[20px] mb-6',
		'shadow-[0px_1px_1px_0px_rgba(0,0,0,0.05),0px_1px_1px_0px_rgba(255,252,240,0.5)_inset,0px_0px_0px_1px_hsla(0,0%,100%,0.1)_inset,0px_0px_1px_0px_rgba(28,27,26,0.5)]',
		'dark:shadow-[0_1px_0_0_rgba(255,255,255,0.03)_inset,0_0_0_1px_rgba(255,255,255,0.03)_inset,0_0_0_1px_rgba(0,0,0,0.1),0_2px_2px_0_rgba(0,0,0,0.1),0_4px_4px_0_rgba(0,0,0,0.1),0_8px_8px_0_rgba(0,0,0,0.1)]',
		className
	)}
>
	<img
		src={src}
		alt={alt}
		width={200}
		height={200}
		class="rounded-[16px] object-cover absolute h-full w-full inset-0"
	/>
	<div class="absolute inset-0 rounded-[16px]">
		<div
			class={cn(
				'absolute inset-0 rounded-[16px]',
				'shadow-[0px_0px_0px_1px_rgba(0,0,0,.07),0px_0px_0px_3px_#fff,0px_0px_0px_4px_rgba(0,0,0,.08)]',
				'dark:shadow-[0px_0px_0px_1px_rgba(0,0,0,.07),0px_0px_0px_3px_rgba(100,100,100,0.3),0px_0px_0px_4px_rgba(0,0,0,.08)]'
			)}
		></div>
		<div
			class={cn(
				'absolute inset-0 rounded-[16px]',
				'dark:shadow-[0px_1px_1px_0px_rgba(0,0,0,0.15),0px_1px_1px_0px_rgba(0,0,0,0.15)_inset,0px_0px_0px_1px_rgba(0,0,0,0.15)_inset,0px_0px_1px_0px_rgba(0,0,0,0.15)]'
			)}
		></div>
	</div>
</div>
