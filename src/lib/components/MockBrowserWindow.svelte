<script lang="ts">
	import { cn } from '$lib/utils/cn';

	interface SidebarItem {
		icon?: string;
		label: string;
		active?: boolean;
		badge?: string | number;
	}

	let {
		class: className = '',
		children,
		size = 'md',
		showSidebar = false,
		sidebarPosition = 'left',
		headerStyle = 'minimal',
		variant = 'generic',
		url,
		sidebarItems,
	}: {
		class?: string;
		children?: import('svelte').Snippet;
		size?: 'sm' | 'md' | 'lg' | 'xl';
		showSidebar?: boolean;
		sidebarPosition?: 'left' | 'right' | 'top' | 'bottom';
		headerStyle?: 'minimal' | 'full';
		variant?: 'chrome' | 'safari' | 'generic' | 'macos' | 'windows';
		url?: string;
		sidebarItems?: SidebarItem[];
	} = $props();

	const sizeClasses: Record<string, string> = {
		sm: 'h-64 max-w-sm',
		md: 'h-80 max-w-2xl',
		lg: 'h-96 max-w-4xl',
		xl: 'h-[32rem] max-w-6xl',
	};

	const sidebarSizes: Record<string, string> = {
		sm: 'w-32',
		md: 'w-48',
		lg: 'w-56',
		xl: 'w-64',
	};

	function getHeaderStyles() {
		const base = 'h-11 border-b border-foreground/5 flex items-center px-4';
		if (variant === 'chrome') return `${base} bg-muted/10 overflow-hidden`;
		if (variant === 'safari') return `${base} bg-muted/10 overflow-hidden border-b border-border/30`;
		return `${base} bg-muted/20`;
	}
</script>

<div
	class={cn(
		'relative mask-b-from-50% rounded-2xl border shadow-[0px_1px_1px_0px_rgba(0,_0,_0,_0.05),_0px_1px_1px_0px_rgba(255,_252,_240,_0.5)_inset,_0px_0px_0px_1px_hsla(0,_0%,_100%,_0.1)_inset,_0px_0px_1px_0px_rgba(28,_27,_26,_0.5)] dark:shadow-[0px_1px_1px_0px_rgba(0,_0,_0,_0.2),_0px_1px_1px_0px_rgba(0,_0,_0,_0.3)_inset,_0px_0px_0px_1px_hsla(0,_0%,_0%,_0.2)_inset,_0px_0px_1px_0px_rgba(255,_255,_255,_0.1)]',
		sizeClasses[size],
		'bg-background border-border',
		className,
		'flex flex-col'
	)}
>
	<!-- Header -->
	<div class={getHeaderStyles()}>
		{#if variant === 'generic' || variant === 'macos' || variant === 'safari'}
			<div class="flex gap-2">
				<div
					class={cn(
						'size-2 rounded-full transition-colors cursor-pointer flex items-center justify-center group',
						headerStyle === 'minimal'
							? 'bg-muted border border-foreground/20'
							: 'bg-red-500 hover:bg-red-600 border border-foreground/20'
					)}
				>
					{#if headerStyle !== 'minimal'}
						<div class="w-1.5 h-0.5 bg-red-900/60 opacity-0 group-hover:opacity-100 transition-opacity"></div>
					{/if}
				</div>
				<div
					class={cn(
						'size-2 rounded-full transition-colors cursor-pointer flex items-center justify-center group',
						headerStyle === 'minimal'
							? 'bg-muted border border-foreground/20'
							: 'bg-yellow-500 hover:bg-yellow-600 border border-foreground/20'
					)}
				>
					{#if headerStyle !== 'minimal'}
						<div class="w-1.5 h-0.5 bg-yellow-900/60 opacity-0 group-hover:opacity-100 transition-opacity"></div>
					{/if}
				</div>
				<div
					class={cn(
						'size-2 rounded-full transition-colors cursor-pointer flex items-center justify-center group',
						headerStyle === 'minimal'
							? 'bg-muted border border-foreground/20'
							: 'bg-green-500 hover:bg-green-600 border border-foreground/20'
					)}
				>
					{#if headerStyle !== 'minimal'}
						<div class="w-1 h-1 border border-green-900/60 opacity-0 group-hover:opacity-100 transition-opacity"></div>
					{/if}
				</div>
			</div>
		{:else if variant === 'windows'}
			<div class="flex gap-1">
				<div class="w-6 h-4 bg-muted/50 hover:bg-muted transition-colors cursor-pointer flex items-center justify-center">
					<div class="w-2 h-0.5 bg-foreground/60"></div>
				</div>
				<div class="w-6 h-4 bg-muted/50 hover:bg-muted transition-colors cursor-pointer flex items-center justify-center">
					<div class="w-2 h-2 border border-foreground/60"></div>
				</div>
				<div class="w-6 h-4 bg-red-500/80 hover:bg-red-500 transition-colors cursor-pointer flex items-center justify-center relative">
					<div class="w-2 h-0.5 bg-white rotate-45 absolute"></div>
					<div class="w-2 h-0.5 bg-white -rotate-45 absolute"></div>
				</div>
			</div>
		{:else if variant === 'chrome'}
			<div class="flex gap-1.5">
				<div class="size-2 rounded-full bg-red-500 hover:bg-red-600 transition-colors cursor-pointer"></div>
				<div class="size-2 rounded-full bg-yellow-500 hover:bg-yellow-600 transition-colors cursor-pointer"></div>
				<div class="size-2 rounded-full bg-green-500 hover:bg-green-600 transition-colors cursor-pointer"></div>
			</div>
		{/if}

		{#if headerStyle === 'full'}
			<div class="flex-1 flex justify-center ml-4">
				<div
					class={cn(
						'px-4 py-2 text-xs text-muted-foreground/70 min-w-[200px] max-w-md flex items-center gap-2 transition-colors',
						variant === 'generic' || variant === 'chrome'
							? 'bg-muted/30 rounded-full border border-foreground/5 shadow-[0px_1px_2px_0px_rgba(0,0,0,0.03)_inset] backdrop-blur-sm'
							: 'bg-muted/20 rounded-lg border border-foreground/5 shadow-[0px_1px_2px_0px_rgba(0,0,0,0.03)_inset] backdrop-blur-sm'
					)}
				>
					{#if url}
						<div class="w-3 h-3 text-muted-foreground/60">
							<svg viewBox="0 0 12 12" fill="currentColor">
								<title>Secure</title>
								<path d="M6 1a2.5 2.5 0 0 1 2.5 2.5V5h.5a1 1 0 0 1 1 1v4a1 1 0 0 1-1 1H3a1 1 0 0 1-1-1V6a1 1 0 0 1 1-1h.5V3.5A2.5 2.5 0 0 1 6 1z" />
							</svg>
						</div>
					{/if}
					<span class="truncate">{url ?? 'https://example.com'}</span>
				</div>
			</div>
		{/if}
	</div>

	<!-- Top Sidebar -->
	{#if showSidebar && sidebarPosition === 'top'}
		<div class="border-b border-foreground/5 bg-muted/20 h-16">
			<div class="p-3 flex-row flex gap-1">
				{#each sidebarItems ?? [{ label: 'Dashboard', active: true }, { label: 'Analytics', badge: '3' }, { label: 'Settings' }, { label: 'Profile' }] as item}
					<div
						class={cn(
							'flex items-center gap-2 px-2 py-1.5 rounded text-sm transition-colors cursor-pointer',
							item.active
								? 'bg-primary/5 text-primary border border-primary/5'
								: 'text-muted-foreground hover:text-foreground hover:bg-muted/20'
						)}
					>
						<span class="flex-1 truncate">{item.label}</span>
						{#if item.badge}
							<div class="bg-primary/5 text-primary text-xs px-1.5 py-0.5 rounded-full min-w-[16px] text-center">
								{item.badge}
							</div>
						{/if}
					</div>
				{/each}
			</div>
		</div>
	{/if}

	<!-- Main Content Area with Sidebars -->
	<div class="flex flex-1 h-0">
		<!-- Left Sidebar -->
		{#if showSidebar && sidebarPosition === 'left'}
			<div class={cn('border-r border-foreground/5 bg-muted/20 flex-shrink-0 h-full', sidebarSizes[size])}>
				<div class="p-3 space-y-1">
					{#each sidebarItems ?? [{ label: 'Dashboard', active: true }, { label: 'Analytics', badge: '3' }, { label: 'Settings' }, { label: 'Profile' }] as item}
						<div
							class={cn(
								'flex items-center gap-2 px-2 py-1.5 rounded text-sm transition-colors cursor-pointer',
								item.active
									? 'bg-primary/5 text-primary border border-primary/5'
									: 'text-muted-foreground hover:text-foreground hover:bg-muted/20'
							)}
						>
							<span class="flex-1 truncate">{item.label}</span>
							{#if item.badge}
								<div class="bg-primary/5 text-primary text-xs px-1.5 py-0.5 rounded-full min-w-[16px] text-center">
									{item.badge}
								</div>
							{/if}
						</div>
					{/each}
				</div>
			</div>
		{/if}

		<!-- Content -->
		<div class="flex-1 relative min-w-0 h-full">
			{@render children?.()}
		</div>

		<!-- Right Sidebar -->
		{#if showSidebar && sidebarPosition === 'right'}
			<div class={cn('border-l border-foreground/5 bg-muted/20 flex-shrink-0 h-full', sidebarSizes[size])}>
				<div class="p-3 space-y-1">
					{#each sidebarItems ?? [{ label: 'Dashboard', active: true }, { label: 'Analytics', badge: '3' }, { label: 'Settings' }, { label: 'Profile' }] as item}
						<div
							class={cn(
								'flex items-center gap-2 px-2 py-1.5 rounded text-sm transition-colors cursor-pointer',
								item.active
									? 'bg-primary/5 text-primary border border-primary/5'
									: 'text-muted-foreground hover:text-foreground hover:bg-muted/20'
							)}
						>
							<span class="flex-1 truncate">{item.label}</span>
							{#if item.badge}
								<div class="bg-primary/5 text-primary text-xs px-1.5 py-0.5 rounded-full min-w-[16px] text-center">
									{item.badge}
								</div>
							{/if}
						</div>
					{/each}
				</div>
			</div>
		{/if}
	</div>

	<!-- Bottom Sidebar -->
	{#if showSidebar && sidebarPosition === 'bottom'}
		<div class="border-t border-foreground/5 bg-muted/20 h-16">
			<div class="p-3 flex-row flex gap-1">
				{#each sidebarItems ?? [{ label: 'Dashboard', active: true }, { label: 'Analytics', badge: '3' }, { label: 'Settings' }, { label: 'Profile' }] as item}
					<div
						class={cn(
							'flex items-center gap-2 px-2 py-1.5 rounded text-sm transition-colors cursor-pointer',
							item.active
								? 'bg-primary/5 text-primary border border-primary/5'
								: 'text-muted-foreground hover:text-foreground hover:bg-muted/20'
						)}
					>
						<span class="flex-1 truncate">{item.label}</span>
						{#if item.badge}
							<div class="bg-primary/5 text-primary text-xs px-1.5 py-0.5 rounded-full min-w-[16px] text-center">
								{item.badge}
							</div>
						{/if}
					</div>
				{/each}
			</div>
		</div>
	{/if}
</div>
