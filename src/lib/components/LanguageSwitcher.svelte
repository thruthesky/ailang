<script lang="ts">
	// 언어 전환 컴포넌트
	// 한국어(ko)와 영어(en) 간 전환을 지원합니다
	import { setLocale, getLocale } from '$lib/paraglide/runtime';
	import { m } from '$lib/paraglide/messages.js';

	// 현재 선택된 언어를 반응형으로 추적
	let currentLocale = $derived(getLocale());
</script>

<!-- 언어 전환 드롭다운 버튼 그룹 -->
<div class="flex items-center gap-2">
	<span class="text-sm text-slate-400">{m.language_switch()}</span>
	<div class="flex rounded-lg overflow-hidden border border-slate-600">
		<!-- 한국어 버튼 -->
		<button
			onclick={() => setLocale('ko')}
			class="px-3 py-1.5 text-sm font-medium transition-colors {currentLocale === 'ko'
				? 'bg-indigo-600 text-white'
				: 'bg-slate-800 text-slate-300 hover:bg-slate-700'}"
		>
			{m.language_ko()}
		</button>
		<!-- 영어 버튼 -->
		<button
			onclick={() => setLocale('en')}
			class="px-3 py-1.5 text-sm font-medium transition-colors {currentLocale === 'en'
				? 'bg-indigo-600 text-white'
				: 'bg-slate-800 text-slate-300 hover:bg-slate-700'}"
		>
			{m.language_en()}
		</button>
	</div>
</div>
