<script lang="ts">
	// AI Lang 메인 홈페이지
	// 인공지능언어의 개념, 배경, 문법, 예시, 표준화 제안서를 포함합니다
	import { m } from '$lib/paraglide/messages.js';
	import CodeBlock from '$lib/components/CodeBlock.svelte';

	// 탭 메뉴 상태 관리
	let activeTab = $state<'basic' | 'code' | 'ask'>('basic');

	// 복사 상태 관리
	let copied = $state(false);

	// 현재 활성화된 탭의 코드 가져오기
	function getCurrentCode(): string {
		if (activeTab === 'basic') return m.grammar_basic_structure();
		if (activeTab === 'code') return m.grammar_example_code();
		return m.grammar_example_ask();
	}

	// 클립보드에 복사하는 함수
	async function copyToClipboard() {
		try {
			await navigator.clipboard.writeText(getCurrentCode());
			copied = true;
			setTimeout(() => {
				copied = false;
			}, 2000);
		} catch (err) {
			console.error('복사 실패:', err);
		}
	}

</script>

<!-- ===== Hero 섹션 ===== -->
<section class="relative overflow-hidden">
	<!-- 배경 그라데이션 효과 -->
	<div class="absolute inset-0 bg-gradient-to-br from-indigo-900/20 via-slate-900 to-slate-900"></div>
	<div class="absolute top-0 left-1/2 -translate-x-1/2 w-[800px] h-[800px] bg-indigo-500/10 rounded-full blur-3xl"></div>

	<div class="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-24 md:py-32">
		<div class="text-center">
			<!-- 메인 타이틀 -->
			<h1 class="text-5xl md:text-7xl font-bold mb-4">
				<span class="text-indigo-400">{m.hero_title()}</span>
			</h1>
			<p class="text-2xl md:text-3xl text-slate-400 mb-6">{m.hero_subtitle()}</p>

			<!-- 태그라인 -->
			<p class="text-xl md:text-2xl text-slate-300 mb-8">{m.hero_tagline()}</p>

			<!-- 설명 -->
			<p class="text-lg text-slate-400 max-w-3xl mx-auto mb-12">
				{m.hero_description()}
			</p>

			<!-- CTA 버튼 -->
			<div class="flex flex-wrap justify-center gap-4">
				<a
					href="#grammar"
					class="px-8 py-3 bg-indigo-600 hover:bg-indigo-500 text-white font-semibold rounded-lg transition-colors"
				>
					{m.hero_cta_grammar()}
				</a>
				<a
					href="#examples"
					class="px-8 py-3 bg-slate-700 hover:bg-slate-600 text-white font-semibold rounded-lg transition-colors"
				>
					{m.hero_cta_examples()}
				</a>
			</div>
		</div>
	</div>
</section>

<!-- ===== 목표 섹션 ===== -->
<section id="goal" class="bg-linear-to-r from-indigo-900/50 to-purple-900/50">
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16">
		<div class="max-w-4xl mx-auto text-center">
			<h2 class="text-3xl md:text-4xl font-bold text-white mb-6">{m.goal_title()}</h2>
			<p class="text-xl text-slate-200 leading-relaxed">
				{m.goal_description()}
			</p>
		</div>
	</div>
</section>

<!-- ===== 정의 섹션 ===== -->
<section id="definition" class="bg-slate-800/50">
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
		<h2 class="text-3xl md:text-4xl font-bold text-center mb-12">{m.definition_title()}</h2>

		<div class="max-w-4xl mx-auto space-y-6">
			<!-- 메인 정의 -->
			<p class="text-lg text-slate-300 leading-relaxed">
				{m.definition_intro()}
			</p>

			<!-- 요약 -->
			<p class="text-lg text-slate-300 leading-relaxed">
				{m.definition_summary()}
			</p>

			<!-- 비유 강조 박스 -->
			<div class="bg-indigo-900/30 border border-indigo-700 rounded-lg p-6 mt-8">
				<p class="text-xl text-indigo-300 font-medium text-center">
					"{m.definition_analogy()}"
				</p>
			</div>
		</div>
	</div>
</section>

<!-- ===== 배경 섹션 ===== -->
<section id="background">
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
		<h2 class="text-3xl md:text-4xl font-bold text-center mb-12">{m.background_title()}</h2>

		<div class="max-w-4xl mx-auto">
			<p class="text-lg text-slate-300 mb-8">{m.background_intro()}</p>

			<!-- AI 입력 구성 요소 목록 -->
			<div class="grid md:grid-cols-2 gap-4 mb-8">
				{#each [
					m.background_item_1(),
					m.background_item_2(),
					m.background_item_3(),
					m.background_item_4(),
					m.background_item_5(),
					m.background_item_6(),
					m.background_item_7(),
					m.background_item_8(),
					m.background_item_9(),
					m.background_item_10(),
					m.background_item_11()
				] as item}
					<div class="flex items-center gap-3 p-4 bg-slate-800 rounded-lg">
						<div class="w-2 h-2 bg-indigo-500 rounded-full"></div>
						<span class="text-slate-300">{item}</span>
					</div>
				{/each}
			</div>

			<!-- 결론 -->
			<p class="text-lg text-slate-300 leading-relaxed">
				{m.background_conclusion()}
			</p>
		</div>
	</div>
</section>

<!-- ===== 비교 섹션 ===== -->
<section id="comparison" class="bg-slate-800/50">
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
		<h2 class="text-3xl md:text-4xl font-bold text-center mb-12">{m.comparison_title()}</h2>

		<!-- 비교 테이블 -->
		<div class="max-w-5xl mx-auto overflow-x-auto">
			<table class="w-full">
				<thead>
					<tr class="bg-slate-700">
						<th class="px-6 py-4 text-left text-slate-200 font-semibold">{m.comparison_header_category()}</th>
						<th class="px-6 py-4 text-left text-slate-200 font-semibold">{m.comparison_header_prompt()}</th>
						<th class="px-6 py-4 text-left text-indigo-300 font-semibold">{m.comparison_header_ailang()}</th>
					</tr>
				</thead>
				<tbody class="divide-y divide-slate-700">
					<!-- 행 1: 기반 -->
					<tr class="hover:bg-slate-700/50">
						<td class="px-6 py-4 text-slate-400 font-medium">{m.comparison_row_1_category()}</td>
						<td class="px-6 py-4 text-slate-300">{m.comparison_row_1_prompt()}</td>
						<td class="px-6 py-4 text-indigo-300">{m.comparison_row_1_ailang()}</td>
					</tr>
					<!-- 행 2: 목표 -->
					<tr class="hover:bg-slate-700/50">
						<td class="px-6 py-4 text-slate-400 font-medium">{m.comparison_row_2_category()}</td>
						<td class="px-6 py-4 text-slate-300">{m.comparison_row_2_prompt()}</td>
						<td class="px-6 py-4 text-indigo-300">{m.comparison_row_2_ailang()}</td>
					</tr>
					<!-- 행 3: 적용 범위 -->
					<tr class="hover:bg-slate-700/50">
						<td class="px-6 py-4 text-slate-400 font-medium">{m.comparison_row_3_category()}</td>
						<td class="px-6 py-4 text-slate-300">{m.comparison_row_3_prompt()}</td>
						<td class="px-6 py-4 text-indigo-300">{m.comparison_row_3_ailang()}</td>
					</tr>
					<!-- 행 4: 역할 -->
					<tr class="hover:bg-slate-700/50">
						<td class="px-6 py-4 text-slate-400 font-medium">{m.comparison_row_4_category()}</td>
						<td class="px-6 py-4 text-slate-300">{m.comparison_row_4_prompt()}</td>
						<td class="px-6 py-4 text-indigo-300">{m.comparison_row_4_ailang()}</td>
					</tr>
					<!-- 행 5: 형태 -->
					<tr class="hover:bg-slate-700/50">
						<td class="px-6 py-4 text-slate-400 font-medium">{m.comparison_row_5_category()}</td>
						<td class="px-6 py-4 text-slate-300">{m.comparison_row_5_prompt()}</td>
						<td class="px-6 py-4 text-indigo-300">{m.comparison_row_5_ailang()}</td>
					</tr>
				</tbody>
			</table>
		</div>
	</div>
</section>

<!-- ===== 핵심 특징 섹션 ===== -->
<section id="features">
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
		<h2 class="text-3xl md:text-4xl font-bold text-center mb-12">{m.features_title()}</h2>

		<!-- 특징 카드 그리드 -->
		<div class="grid md:grid-cols-2 gap-6 max-w-5xl mx-auto">
			<!-- 특징 1: AI 친화적 구조화 -->
			<div class="bg-slate-800 rounded-xl p-6 border border-slate-700 hover:border-indigo-600 transition-colors">
				<div class="w-12 h-12 bg-indigo-600/20 rounded-lg flex items-center justify-center mb-4">
					<svg class="w-6 h-6 text-indigo-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 10h16M4 14h16M4 18h16" />
					</svg>
				</div>
				<h3 class="text-xl font-bold text-slate-100 mb-2">{m.feature_1_title()}</h3>
				<p class="text-sm text-indigo-400 mb-3">{m.feature_1_subtitle()}</p>
				<p class="text-slate-400">{m.feature_1_desc()}</p>
			</div>

			<!-- 특징 2: AI 시스템 레이어 반영 -->
			<div class="bg-slate-800 rounded-xl p-6 border border-slate-700 hover:border-indigo-600 transition-colors">
				<div class="w-12 h-12 bg-indigo-600/20 rounded-lg flex items-center justify-center mb-4">
					<svg class="w-6 h-6 text-indigo-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10" />
					</svg>
				</div>
				<h3 class="text-xl font-bold text-slate-100 mb-2">{m.feature_2_title()}</h3>
				<p class="text-sm text-indigo-400 mb-3">{m.feature_2_subtitle()}</p>
				<p class="text-slate-400">{m.feature_2_desc()}</p>
			</div>

			<!-- 특징 3: 확장 가능한 메타언어 -->
			<div class="bg-slate-800 rounded-xl p-6 border border-slate-700 hover:border-indigo-600 transition-colors">
				<div class="w-12 h-12 bg-indigo-600/20 rounded-lg flex items-center justify-center mb-4">
					<svg class="w-6 h-6 text-indigo-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 9l3 3-3 3m5 0h3M5 20h14a2 2 0 002-2V6a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
					</svg>
				</div>
				<h3 class="text-xl font-bold text-slate-100 mb-2">{m.feature_3_title()}</h3>
				<p class="text-sm text-indigo-400 mb-3">{m.feature_3_subtitle()}</p>
				<p class="text-slate-400">{m.feature_3_desc()}</p>
			</div>

			<!-- 특징 4: 의도→행위 손실 최소화 -->
			<div class="bg-slate-800 rounded-xl p-6 border border-slate-700 hover:border-indigo-600 transition-colors">
				<div class="w-12 h-12 bg-indigo-600/20 rounded-lg flex items-center justify-center mb-4">
					<svg class="w-6 h-6 text-indigo-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
					</svg>
				</div>
				<h3 class="text-xl font-bold text-slate-100 mb-2">{m.feature_4_title()}</h3>
				<p class="text-sm text-indigo-400 mb-3">{m.feature_4_subtitle()}</p>
				<p class="text-slate-400">{m.feature_4_desc()}</p>
			</div>
		</div>
	</div>
</section>

<!-- ===== 문법 섹션 ===== -->
<section id="grammar" class="bg-slate-800/50">
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
		<h2 class="text-3xl md:text-4xl font-bold text-center mb-6">{m.grammar_title()}</h2>
		<p class="text-lg text-slate-400 text-center max-w-3xl mx-auto mb-12">{m.grammar_intro()}</p>

		<div class="max-w-5xl mx-auto space-y-12">
			<!-- 기본 구조 - 탭 메뉴 포함 -->
			<div>
				<h3 class="text-2xl font-bold text-slate-100 mb-6">{m.grammar_structure_title()}</h3>

				<!-- 탭 메뉴 + 복사 버튼 -->
				<div class="flex flex-wrap items-center justify-between gap-2 mb-4">
					<!-- 탭 버튼들 -->
					<div class="flex flex-wrap gap-2">
						<button
							onclick={() => activeTab = 'basic'}
							class="px-4 py-2 rounded-lg text-sm font-medium transition-colors {activeTab === 'basic' ? 'bg-indigo-600 text-white' : 'bg-slate-700 text-slate-300 hover:bg-slate-600'}"
						>
							{m.grammar_tab_basic()}
						</button>
						<button
							onclick={() => activeTab = 'code'}
							class="px-4 py-2 rounded-lg text-sm font-medium transition-colors {activeTab === 'code' ? 'bg-indigo-600 text-white' : 'bg-slate-700 text-slate-300 hover:bg-slate-600'}"
						>
							{m.grammar_tab_example_code()}
						</button>
						<button
							onclick={() => activeTab = 'ask'}
							class="px-4 py-2 rounded-lg text-sm font-medium transition-colors {activeTab === 'ask' ? 'bg-indigo-600 text-white' : 'bg-slate-700 text-slate-300 hover:bg-slate-600'}"
						>
							{m.grammar_tab_example_ask()}
						</button>
					</div>

					<!-- 복사 버튼 -->
					<button
						onclick={copyToClipboard}
						class="px-4 py-2 rounded-lg text-sm font-medium transition-colors flex items-center gap-2 {copied ? 'bg-emerald-600 text-white' : 'bg-slate-700 text-slate-300 hover:bg-slate-600'}"
					>
						{#if copied}
							<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
							</svg>
							{m.grammar_copied()}
						{:else}
							<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z" />
							</svg>
							{m.grammar_copy_button()}
						{/if}
					</button>
				</div>

				<!-- 탭 콘텐츠 -->
				{#if activeTab === 'basic'}
					<CodeBlock code={m.grammar_basic_structure()} title={m.grammar_tab_basic()} />
				{:else if activeTab === 'code'}
					<CodeBlock code={m.grammar_example_code()} title={m.grammar_tab_example_code()} />
				{:else}
					<CodeBlock code={m.grammar_example_ask()} title={m.grammar_tab_example_ask()} />
				{/if}
			</div>

			<!-- 핵심 키워드 설명 -->
			<div>
				<h3 class="text-2xl font-bold text-slate-100 mb-6">{m.grammar_directives_title()}</h3>
				<div class="grid md:grid-cols-2 lg:grid-cols-3 gap-4">
					<div class="bg-slate-800 rounded-lg p-4 border border-slate-700">
						<code class="text-indigo-400 font-semibold">{m.grammar_key_intent()}</code>
						<span class="ml-1 text-emerald-400 font-bold text-sm">{m.grammar_key_intent_required()}</span>
						<p class="text-slate-400 mt-2">{m.grammar_directive_intent()}</p>
					</div>
					<div class="bg-slate-800 rounded-lg p-4 border border-slate-700">
						<code class="text-indigo-400 font-semibold">{m.grammar_key_reason()}</code>
						<p class="text-slate-400 mt-2">{m.grammar_directive_reason()}</p>
					</div>
					<div class="bg-slate-800 rounded-lg p-4 border border-slate-700">
						<code class="text-indigo-400 font-semibold">{m.grammar_key_persona()}</code>
						<p class="text-slate-400 mt-2">{m.grammar_directive_persona()}</p>
					</div>
					<div class="bg-slate-800 rounded-lg p-4 border border-slate-700">
						<code class="text-indigo-400 font-semibold">{m.grammar_key_context()}</code>
						<p class="text-slate-400 mt-2">{m.grammar_directive_context()}</p>
					</div>
					<div class="bg-slate-800 rounded-lg p-4 border border-slate-700">
						<code class="text-indigo-400 font-semibold">{m.grammar_key_current_state()}</code>
						<p class="text-slate-400 mt-2">{m.grammar_directive_current_state()}</p>
					</div>
					<div class="bg-slate-800 rounded-lg p-4 border border-slate-700">
						<code class="text-indigo-400 font-semibold">{m.grammar_key_reproduce()}</code>
						<p class="text-slate-400 mt-2">{m.grammar_directive_reproduce()}</p>
					</div>
					<div class="bg-slate-800 rounded-lg p-4 border border-slate-700">
						<code class="text-indigo-400 font-semibold">{m.grammar_key_expected_result()}</code>
						<p class="text-slate-400 mt-2">{m.grammar_directive_expected_result()}</p>
					</div>
					<div class="bg-slate-800 rounded-lg p-4 border border-slate-700">
						<code class="text-indigo-400 font-semibold">{m.grammar_key_guidelines()}</code>
						<p class="text-slate-400 mt-2">{m.grammar_directive_guidelines()}</p>
					</div>
					<div class="bg-slate-800 rounded-lg p-4 border border-slate-700">
						<code class="text-indigo-400 font-semibold">{m.grammar_key_constraints()}</code>
						<p class="text-slate-400 mt-2">{m.grammar_directive_constraints()}</p>
					</div>
					<div class="bg-slate-800 rounded-lg p-4 border border-slate-700">
						<code class="text-indigo-400 font-semibold">{m.grammar_key_output()}</code>
						<p class="text-slate-400 mt-2">{m.grammar_directive_output()}</p>
					</div>
					<div class="bg-slate-800 rounded-lg p-4 border border-slate-700">
						<code class="text-indigo-400 font-semibold">{m.grammar_key_style()}</code>
						<p class="text-slate-400 mt-2">{m.grammar_directive_style()}</p>
					</div>
				</div>
			</div>

			<!-- 의도 유형 예시 -->
			<div>
				<h3 class="text-2xl font-bold text-slate-100 mb-6">{m.grammar_intent_types_title()}</h3>
				<div class="grid sm:grid-cols-2 gap-3">
					{#each [
						m.grammar_intent_create(),
						m.grammar_intent_update(),
						m.grammar_intent_transform(),
						m.grammar_intent_analyze(),
						m.grammar_intent_explain(),
						m.grammar_intent_validate(),
						m.grammar_intent_debug(),
						m.grammar_intent_troubleshoot(),
						m.grammar_intent_migrate(),
						m.grammar_intent_decide()
					] as example}
						<div class="bg-slate-800 rounded-lg px-4 py-3 border border-slate-700">
							<code class="text-slate-300 text-sm">{example}</code>
						</div>
					{/each}
				</div>
			</div>

			<!-- 구문 규칙 -->
			<div>
				<h3 class="text-2xl font-bold text-slate-100 mb-6">{m.grammar_syntax_title()}</h3>
				<ul class="space-y-3">
					{#each [
						m.grammar_syntax_1(),
						m.grammar_syntax_2(),
						m.grammar_syntax_3(),
						m.grammar_syntax_4(),
						m.grammar_syntax_5(),
						m.grammar_syntax_6()
					] as rule, i}
						<li class="flex items-start gap-3">
							<span class="flex-shrink-0 w-6 h-6 bg-indigo-600 rounded-full flex items-center justify-center text-sm font-bold">{i + 1}</span>
							<span class="text-slate-300">{rule}</span>
						</li>
					{/each}
				</ul>
			</div>
		</div>
	</div>
</section>

<!-- ===== 프롬프트 엔지니어링 기법 섹션 ===== -->
<section id="techniques">
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
		<h2 class="text-3xl md:text-4xl font-bold text-center mb-6">{m.techniques_title()}</h2>
		<p class="text-lg text-slate-400 text-center max-w-4xl mx-auto mb-8">{m.techniques_intro()}</p>

		<!-- 핵심 개념 박스 -->
		<div class="max-w-4xl mx-auto mb-12 space-y-4">
			<div class="bg-indigo-900/30 border border-indigo-700 rounded-lg p-6">
				<p class="text-indigo-300">{m.techniques_core_concept()}</p>
			</div>
			<div class="grid md:grid-cols-2 gap-4">
				<div class="bg-slate-800 rounded-lg p-4 border border-slate-700">
					<p class="text-slate-300">{m.techniques_prompt_def()}</p>
				</div>
				<div class="bg-slate-800 rounded-lg p-4 border border-slate-700">
					<p class="text-slate-300 text-sm">{m.techniques_llm_mechanism()}</p>
				</div>
			</div>
		</div>

		<!-- 기법 목록 -->
		<div class="max-w-5xl mx-auto grid md:grid-cols-2 gap-6">
			<!-- 1. Persona -->
			<div class="bg-slate-800 rounded-xl p-6 border border-slate-700">
				<h3 class="text-lg font-bold text-indigo-400 mb-2">{m.technique_1_name()}</h3>
				<p class="text-slate-400 text-sm mb-3">{m.technique_1_desc()}</p>
				<code class="text-xs text-emerald-400 bg-slate-900 px-2 py-1 rounded">{m.technique_1_pattern()}</code>
			</div>

			<!-- 2. System Prompt -->
			<div class="bg-slate-800 rounded-xl p-6 border border-slate-700">
				<h3 class="text-lg font-bold text-indigo-400 mb-2">{m.technique_2_name()}</h3>
				<p class="text-slate-400 text-sm">{m.technique_2_desc()}</p>
			</div>

			<!-- 3. User Prompt -->
			<div class="bg-slate-800 rounded-xl p-6 border border-slate-700">
				<h3 class="text-lg font-bold text-indigo-400 mb-2">{m.technique_3_name()}</h3>
				<p class="text-slate-400 text-sm">{m.technique_3_desc()}</p>
			</div>

			<!-- 4. Context -->
			<div class="bg-slate-800 rounded-xl p-6 border border-slate-700">
				<h3 class="text-lg font-bold text-indigo-400 mb-2">{m.technique_4_name()}</h3>
				<p class="text-slate-400 text-sm">{m.technique_4_desc()}</p>
			</div>

			<!-- 5. BreadCrumb -->
			<div class="bg-slate-800 rounded-xl p-6 border border-slate-700">
				<h3 class="text-lg font-bold text-indigo-400 mb-2">{m.technique_5_name()}</h3>
				<p class="text-slate-400 text-sm mb-3">{m.technique_5_desc()}</p>
				<code class="text-xs text-emerald-400 bg-slate-900 px-2 py-1 rounded">{m.technique_5_example()}</code>
			</div>

			<!-- 6. Output Format -->
			<div class="bg-slate-800 rounded-xl p-6 border border-slate-700">
				<h3 class="text-lg font-bold text-indigo-400 mb-2">{m.technique_6_name()}</h3>
				<p class="text-slate-400 text-sm">{m.technique_6_desc()}</p>
			</div>

			<!-- 7. COT -->
			<div class="bg-slate-800 rounded-xl p-6 border border-slate-700">
				<h3 class="text-lg font-bold text-indigo-400 mb-2">{m.technique_7_name()}</h3>
				<p class="text-slate-400 text-sm mb-3">{m.technique_7_desc()}</p>
				<code class="text-xs text-emerald-400 bg-slate-900 px-2 py-1 rounded">{m.technique_7_pattern()}</code>
			</div>

			<!-- 8. TOT -->
			<div class="bg-slate-800 rounded-xl p-6 border border-slate-700">
				<h3 class="text-lg font-bold text-indigo-400 mb-2">{m.technique_8_name()}</h3>
				<p class="text-slate-400 text-sm mb-3">{m.technique_8_desc()}</p>
				<code class="text-xs text-emerald-400 bg-slate-900 px-2 py-1 rounded block">{m.technique_8_pattern()}</code>
			</div>

			<!-- 9. Task Decomposition -->
			<div class="bg-slate-800 rounded-xl p-6 border border-slate-700">
				<h3 class="text-lg font-bold text-indigo-400 mb-2">{m.technique_9_name()}</h3>
				<p class="text-slate-400 text-sm mb-3">{m.technique_9_desc()}</p>
				<code class="text-xs text-emerald-400 bg-slate-900 px-2 py-1 rounded">{m.technique_9_pattern()}</code>
			</div>

			<!-- 10. 6하 원칙 -->
			<div class="bg-slate-800 rounded-xl p-6 border border-slate-700">
				<h3 class="text-lg font-bold text-indigo-400 mb-2">{m.technique_10_name()}</h3>
				<p class="text-slate-400 text-sm">{m.technique_10_desc()}</p>
			</div>

			<!-- 11. Tone and Style -->
			<div class="bg-slate-800 rounded-xl p-6 border border-slate-700 md:col-span-2">
				<h3 class="text-lg font-bold text-indigo-400 mb-2">{m.technique_11_name()}</h3>
				<p class="text-slate-400 text-sm mb-3">{m.technique_11_desc()}</p>
				<code class="text-xs text-emerald-400 bg-slate-900 px-2 py-1 rounded">{m.technique_11_pattern()}</code>
			</div>
		</div>
	</div>
</section>

<!-- ===== 예시 섹션 ===== -->
<section id="examples" class="bg-slate-800/50">
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
		<h2 class="text-3xl md:text-4xl font-bold text-center mb-12">{m.examples_title()}</h2>

		<div class="max-w-5xl mx-auto space-y-8">
			<!-- 예시 1: 코드 생성 -->
			<div>
				<h3 class="text-xl font-bold text-slate-100 mb-2">{m.example_1_title()}</h3>
				<p class="text-slate-400 mb-4">{m.example_1_desc()}</p>
				<CodeBlock code={m.example_1_code()} title={m.example_1_title()} />
			</div>

			<!-- 예시 2: 문서 분석 -->
			<div>
				<h3 class="text-xl font-bold text-slate-100 mb-2">{m.example_2_title()}</h3>
				<p class="text-slate-400 mb-4">{m.example_2_desc()}</p>
				<CodeBlock code={m.example_2_code()} title={m.example_2_title()} />
			</div>

			<!-- 예시 3: 콘텐츠 변환 -->
			<div>
				<h3 class="text-xl font-bold text-slate-100 mb-2">{m.example_3_title()}</h3>
				<p class="text-slate-400 mb-4">{m.example_3_desc()}</p>
				<CodeBlock code={m.example_3_code()} title={m.example_3_title()} />
			</div>
		</div>
	</div>
</section>

<!-- ===== 표준화 제안서 섹션 ===== -->
<section id="spec" class="bg-slate-800/50">
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
		<h2 class="text-3xl md:text-4xl font-bold text-center mb-4">{m.spec_title()}</h2>
		<p class="text-lg text-indigo-400 text-center mb-12">{m.spec_version()}</p>

		<div class="max-w-4xl mx-auto prose prose-invert prose-slate">
			<!-- 1. 개요 -->
			<div class="mb-12">
				<h3 class="text-2xl font-bold text-slate-100 mb-6">{m.spec_section_1_title()}</h3>

				<div class="space-y-6">
					<div>
						<h4 class="text-lg font-semibold text-slate-200 mb-2">{m.spec_section_1_1()}</h4>
						<p class="text-slate-400">{m.spec_section_1_1_content()}</p>
					</div>

					<div>
						<h4 class="text-lg font-semibold text-slate-200 mb-2">{m.spec_section_1_2()}</h4>
						<p class="text-slate-400">{m.spec_section_1_2_content()}</p>
					</div>

					<div>
						<h4 class="text-lg font-semibold text-slate-200 mb-2">{m.spec_section_1_3()}</h4>
						<ul class="space-y-2 text-slate-400">
							<li><strong class="text-slate-300">{m.spec_term_directive()}</strong></li>
							<li><strong class="text-slate-300">{m.spec_term_block()}</strong></li>
							<li><strong class="text-slate-300">{m.spec_term_intent()}</strong></li>
						</ul>
					</div>
				</div>
			</div>

			<!-- 2. 핵심 개념 -->
			<div class="mb-12">
				<h3 class="text-2xl font-bold text-slate-100 mb-4">{m.spec_section_2_title()}</h3>
				<p class="text-slate-400">{m.spec_section_2_content()}</p>
			</div>

			<!-- 3. 구문 규칙 -->
			<div class="mb-12">
				<h3 class="text-2xl font-bold text-slate-100 mb-4">{m.spec_section_3_title()}</h3>
				<p class="text-slate-400">{m.spec_section_3_content()}</p>
			</div>

			<!-- 4. 예약어 -->
			<div class="mb-12">
				<h3 class="text-2xl font-bold text-slate-100 mb-4">{m.spec_section_4_title()}</h3>
				<p class="text-slate-400">{m.spec_section_4_content()}</p>
			</div>

			<!-- 5. 확장성 -->
			<div class="mb-12">
				<h3 class="text-2xl font-bold text-slate-100 mb-4">{m.spec_section_5_title()}</h3>
				<p class="text-slate-400">{m.spec_section_5_content()}</p>
			</div>
		</div>
	</div>
</section>
