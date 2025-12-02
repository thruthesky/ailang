<script lang="ts">
	// 언어 전환 컴포넌트
	// 한국어(ko), 영어(en), 중국어(zh-Hans), 일본어(ja), 스페인어(es) 간 전환을 지원합니다
	// variant="dropdown"이면 드롭다운 메뉴, 기본값은 버튼 그룹
	import { setLocale, getLocale } from '$lib/paraglide/runtime';
	import { m } from '$lib/paraglide/messages.js';

	// Props: variant가 "dropdown"이면 드롭다운 메뉴로 표시
	let { variant = 'buttons' }: { variant?: 'buttons' | 'dropdown' } = $props();

	// 현재 선택된 언어를 반응형으로 추적
	let currentLocale = $derived(getLocale());

	// 드롭다운 열림 상태
	let isOpen = $state(false);

	// 지원하는 언어 목록
	const languages = [
		{ code: 'ko', label: () => m.language_ko() },
		{ code: 'en', label: () => m.language_en() },
		{ code: 'zh-Hans', label: () => m.language_zh_Hans() },
		{ code: 'ja', label: () => m.language_ja() },
		{ code: 'es', label: () => m.language_es() }
	] as const;

	// 현재 언어의 라벨 가져오기
	function getCurrentLabel() {
		const current = languages.find((lang) => lang.code === currentLocale);
		return current ? current.label() : 'Language';
	}

	// 언어 선택 핸들러
	function selectLanguage(code: string) {
		setLocale(code);
		isOpen = false;
	}

	// 드롭다운 외부 클릭 시 닫기
	function handleClickOutside(event: MouseEvent) {
		const target = event.target as HTMLElement;
		if (!target.closest('.language-dropdown')) {
			isOpen = false;
		}
	}
</script>

<svelte:window onclick={handleClickOutside} />

{#if variant === 'dropdown'}
	<!-- 드롭다운 메뉴 (데스크톱용) -->
	<div class="language-dropdown relative">
		<button
			onclick={(e) => {
				e.stopPropagation();
				isOpen = !isOpen;
			}}
			class="flex items-center gap-2 px-3 py-2 text-sm text-slate-300 hover:text-white hover:bg-slate-800 rounded-md transition-colors"
		>
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path
					stroke-linecap="round"
					stroke-linejoin="round"
					stroke-width="2"
					d="M21 12a9 9 0 01-9 9m9-9a9 9 0 00-9-9m9 9H3m9 9a9 9 0 01-9-9m9 9c1.657 0 3-4.03 3-9s-1.343-9-3-9m0 18c-1.657 0-3-4.03-3-9s1.343-9 3-9m-9 9a9 9 0 019-9"
				/>
			</svg>
			<span>{getCurrentLabel()}</span>
			<svg
				class="w-4 h-4 transition-transform {isOpen ? 'rotate-180' : ''}"
				fill="none"
				stroke="currentColor"
				viewBox="0 0 24 24"
			>
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
			</svg>
		</button>

		{#if isOpen}
			<div
				class="absolute right-0 top-full mt-1 py-1 bg-slate-800 border border-slate-600 rounded-lg shadow-xl min-w-[140px] z-50"
			>
				{#each languages as lang}
					<button
						onclick={() => selectLanguage(lang.code)}
						class="w-full px-4 py-2 text-left text-sm transition-colors {currentLocale === lang.code
							? 'bg-indigo-600 text-white'
							: 'text-slate-300 hover:bg-slate-700 hover:text-white'}"
					>
						{lang.label()}
					</button>
				{/each}
			</div>
		{/if}
	</div>
{:else}
	<!-- 버튼 그룹 (모바일용) -->
	<div class="flex items-center gap-2 flex-wrap">
		<span class="text-sm text-slate-400">{m.language_switch()}</span>
		<div class="flex flex-wrap rounded-lg overflow-hidden border border-slate-600">
			{#each languages as lang}
				<button
					onclick={() => setLocale(lang.code)}
					class="px-3 py-1.5 text-sm font-medium transition-colors {currentLocale === lang.code
						? 'bg-indigo-600 text-white'
						: 'bg-slate-800 text-slate-300 hover:bg-slate-700'}"
				>
					{lang.label()}
				</button>
			{/each}
		</div>
	</div>
{/if}
