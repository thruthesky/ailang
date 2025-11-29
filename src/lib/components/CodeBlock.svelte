<script lang="ts">
	// 코드 블록 컴포넌트
	// AI Lang 예시 코드를 구문 하이라이팅과 함께 표시합니다

	interface Props {
		code: string;        // 표시할 코드 문자열
		title?: string;      // 코드 블록 제목 (선택)
		language?: string;   // 언어 표시 (기본값: ailang)
	}

	let { code, title = '', language = 'ailang' }: Props = $props();

	// 간단한 AI Lang 구문 하이라이팅
	// @ 지시어, 키워드, 값 등을 색상으로 구분합니다
	function highlightCode(code: string): string {
		return code
			// @ 지시어 하이라이팅 (파란색)
			.replace(/(@\w+)/g, '<span class="text-indigo-400 font-semibold">$1</span>')
			// 중괄호 하이라이팅 (노란색)
			.replace(/([{}])/g, '<span class="text-yellow-400">$1</span>')
			// 대괄호 하이라이팅 (초록색)
			.replace(/(\[|\])/g, '<span class="text-emerald-400">$1</span>')
			// 키 하이라이팅 (회색) - 콜론 앞의 단어
			.replace(/(\s)(\w+)(:)/g, '$1<span class="text-slate-400">$2</span>$3')
			// 주석 스타일의 자연어 부분 (연한 색상)
			.replace(/(#.*$)/gm, '<span class="text-slate-500 italic">$1</span>');
	}
</script>

<!-- 코드 블록 컨테이너 -->
<div class="rounded-lg overflow-hidden bg-slate-800/50 border border-slate-700">
	<!-- 헤더 (제목과 언어 표시) -->
	{#if title || language}
		<div class="flex items-center justify-between px-4 py-2 bg-slate-800 border-b border-slate-700">
			{#if title}
				<span class="text-sm font-medium text-slate-300">{title}</span>
			{:else}
				<span></span>
			{/if}
			<span class="text-xs text-slate-500 uppercase tracking-wider">{language}</span>
		</div>
	{/if}

	<!-- 코드 내용 -->
	<pre class="p-4 overflow-x-auto text-sm leading-relaxed"><code class="font-mono text-slate-200">{@html highlightCode(code)}</code></pre>
</div>
