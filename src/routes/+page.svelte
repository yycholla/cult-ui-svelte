<script lang="ts">
	import {
		AnimatedNumber,
		CosmicButton,
		DitherImage,
		DitherImageCaption,
		DitherImageContent,
		DitherImageFrame,
		DitherImageOverlay,
		DitherImageReveal,
		Dock,
		DockItem,
		DynamicIsland,
		GlowButton,
		GradientHeading,
		MinimalCard,
		MinimalCardContent,
		MinimalCardDescription,
		MinimalCardFooter,
		MinimalCardImage,
		MinimalCardTitle,
		MockBrowserWindow
	} from '$lib';

	let islandPreset = $state<'default' | 'compact' | 'medium' | 'tall'>('default');

	const sidebarItems = [
		{ label: 'Dashboard', active: true, icon: '⌘' },
		{ label: 'Agents', badge: 7, icon: '✦' },
		{ label: 'Settings', icon: '⚙' }
	];
</script>

<svelte:head>
	<title>cult-ui-svelte</title>
	<meta
		name="description"
		content="A Svelte-native port of selected cult-ui design engineering components."
	/>
</svelte:head>

<main class="mx-auto flex min-h-screen w-full max-w-6xl flex-col gap-16 px-6 py-12">
	<section class="grid gap-8 lg:grid-cols-[1.15fr_0.85fr] lg:items-center">
		<div class="space-y-6">
			<p class="text-sm uppercase tracking-[0.35em] text-lime-300/80">cult-ui → Svelte 5</p>
			<GradientHeading as="h1" size="xxl" weight="black">
				Design-engineering components, Svelte-native.
			</GradientHeading>
			<p class="max-w-2xl text-lg leading-8 text-slate-300">
				This package ports a practical first slice of cult-ui into Svelte 5 runes,
				Tailwind CSS v4, snippets, and Svelte motion — no React wrapper layer.
			</p>
			<div class="flex flex-wrap gap-4">
				<CosmicButton href="https://github.com/nolly-studio/cult-ui">Original cult-ui</CosmicButton>
				<GlowButton text="Svelte Port" href="https://svelte.dev" />
			</div>
		</div>

		<MinimalCard class="mx-auto max-w-sm">
			<MinimalCardImage
				src="https://images.unsplash.com/photo-1550745165-9bc0b252726f?auto=format&fit=crop&w=900&q=80"
				alt="Retro terminal setup"
			/>
			<MinimalCardContent>
				<MinimalCardTitle>Copy-paste aesthetics</MinimalCardTitle>
				<MinimalCardDescription>
					Svelte snippets replace React children while keeping the original Tailwind-heavy visual language.
				</MinimalCardDescription>
			</MinimalCardContent>
			<MinimalCardFooter>
				<span class="text-sm text-slate-400">Components ported</span>
				<strong><AnimatedNumber value={20} /></strong>
			</MinimalCardFooter>
		</MinimalCard>
	</section>

	<section class="grid gap-8 lg:grid-cols-2">
		<div class="space-y-4 rounded-3xl border border-white/10 bg-white/[0.03] p-6">
			<GradientHeading as="h2" size="lg">Dynamic Island</GradientHeading>
			<div class="flex flex-wrap gap-2">
				{#each ['default', 'compact', 'medium', 'tall'] as preset (preset)}
					<button
						class="rounded-full border border-white/10 px-3 py-1 text-sm text-slate-200 transition hover:bg-white/10"
						onclick={() => (islandPreset = preset as typeof islandPreset)}
					>
						{preset}
					</button>
				{/each}
			</div>
			<DynamicIsland preset={islandPreset} class="mt-8">
				<div class="px-5 text-sm text-lime-200">
					<strong>Preset:</strong> {islandPreset}
				</div>
			</DynamicIsland>
		</div>

		<MockBrowserWindow
			size="lg"
			variant="safari"
			url="cult-ui-svelte.local"
			showSidebar
			{sidebarItems}
		>
			<div class="flex h-full flex-col justify-center gap-4 p-8">
				<GradientHeading as="h3" size="md">Registry preview</GradientHeading>
				<p class="max-w-md text-sm leading-6 text-slate-300">
					The demo route doubles as a visual smoke test for package exports and component composition.
				</p>
			</div>
		</MockBrowserWindow>
	</section>

	<section class="grid gap-8 lg:grid-cols-[0.8fr_1.2fr] lg:items-center">
		<DitherImage>
			<DitherImageFrame aspectRatio="video" size="lg" class="overflow-hidden bg-black">
				<DitherImageReveal class="h-full w-full">
					<DitherImageContent
						src="https://images.unsplash.com/photo-1519608487953-e999c86e7455?auto=format&fit=crop&w=1200&q=80"
						alt="Neon city at night"
					/>
					<DitherImageOverlay
						src="https://images.unsplash.com/photo-1519608487953-e999c86e7455?auto=format&fit=crop&w=1200&q=80"
						alt="Clean neon city reveal"
						direction="radial"
						from={0}
						to={70}
					/>
				</DitherImageReveal>
			</DitherImageFrame>
			<DitherImageCaption>Native image port of the original Next/Image dither compound component.</DitherImageCaption>
		</DitherImage>

		<div class="relative min-h-48 rounded-3xl border border-white/10 bg-white/[0.03] p-6">
			<GradientHeading as="h2" size="lg">Dock</GradientHeading>
			<p class="max-w-xl text-sm leading-6 text-slate-300">
				Hover the dock items for proximity scaling. Click an item to toggle the bounce indicator.
			</p>
			<Dock>
				<DockItem id={0} class="grid size-12 place-items-center text-2xl">⌘</DockItem>
				<DockItem id={1} class="grid size-12 place-items-center text-2xl">✦</DockItem>
				<DockItem id={2} class="grid size-12 place-items-center text-2xl">⚙</DockItem>
			</Dock>
		</div>
	</section>

	<section class="rounded-3xl border border-lime-300/20 bg-lime-300/[0.04] p-6 text-sm leading-7 text-slate-300">
		<strong class="text-lime-200">Port status:</strong> first Svelte-native slice includes buttons,
		headings, cards, browser window, animated number, dither image, dock, and dynamic island.
	</section>
</main>
