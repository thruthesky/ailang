<script lang="ts">
	// 네비게이션 컴포넌트
	// 상단 고정 네비게이션 바와 섹션 링크를 제공합니다
	import { m } from '$lib/paraglide/messages.js';
	import LanguageSwitcher from './LanguageSwitcher.svelte';

	// 모바일 메뉴 상태
	let mobileMenuOpen = $state(false);

	// 네비게이션 항목 정의
	// id는 해당 섹션의 HTML id와 일치해야 합니다
	const navItems = [
		{ id: 'definition', label: () => m.nav_definition() },
		{ id: 'background', label: () => m.nav_background() },
		{ id: 'comparison', label: () => m.nav_comparison() },
		{ id: 'features', label: () => m.nav_features() },
		{ id: 'grammar', label: () => m.nav_grammar() },
		{ id: 'techniques', label: () => m.nav_techniques() },
		{ id: 'examples', label: () => m.nav_examples() },
		{ id: 'spec', label: () => m.nav_spec() }
	];

	// 부드러운 스크롤로 섹션 이동
	function scrollToSection(id: string) {
		const element = document.getElementById(id);
		if (element) {
			element.scrollIntoView({ behavior: 'smooth' });
			mobileMenuOpen = false;
		}
	}
</script>

<!-- 상단 고정 네비게이션 바 -->
<nav class="sticky top-0 z-50 bg-slate-900/95 backdrop-blur-sm border-b border-slate-700">
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="flex items-center justify-between h-16">
			<!-- 로고 및 사이트 이름 -->
			<a href="/" class="flex items-center gap-2">
				<span class="text-2xl font-bold text-indigo-400">AI</span>
				<span class="text-xl font-semibold text-white">Lang</span>
			</a>

			<!-- 데스크톱 네비게이션 링크 -->
			<div class="hidden lg:flex items-center gap-1">
				{#each navItems as item}
					<button
						onclick={() => scrollToSection(item.id)}
						class="px-3 py-2 text-sm text-slate-300 hover:text-white hover:bg-slate-800 rounded-md transition-colors"
					>
						{item.label()}
					</button>
				{/each}
			</div>

			<!-- 언어 전환 (데스크톱) -->
			<div class="hidden lg:block">
				<LanguageSwitcher />
			</div>

			<!-- 모바일 메뉴 버튼 -->
			<button
				onclick={() => (mobileMenuOpen = !mobileMenuOpen)}
				class="lg:hidden p-2 text-slate-300 hover:text-white"
				aria-label="메뉴 열기/닫기"
			>
				<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					{#if mobileMenuOpen}
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
					{:else}
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
					{/if}
				</svg>
			</button>
		</div>
	</div>

	<!-- 모바일 메뉴 -->
	{#if mobileMenuOpen}
		<div class="lg:hidden bg-slate-800 border-t border-slate-700">
			<div class="px-4 py-3 space-y-1">
				{#each navItems as item}
					<button
						onclick={() => scrollToSection(item.id)}
						class="block w-full text-left px-3 py-2 text-slate-300 hover:text-white hover:bg-slate-700 rounded-md"
					>
						{item.label()}
					</button>
				{/each}
				<div class="pt-3 border-t border-slate-700">
					<LanguageSwitcher />
				</div>
			</div>
		</div>
	{/if}
</nav>
