<script lang="ts">
	// 푸터 컴포넌트
	// 사이트 하단에 버전, 라이선스, 저작권 정보를 표시합니다
	import { m } from '$lib/paraglide/messages.js';
</script>

<!-- 푸터 영역 -->
<footer class="bg-slate-900 border-t border-slate-800">
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
		<div class="flex flex-col gap-6">
			<!-- 상단: 로고, 링크들 -->
			<div class="flex flex-col md:flex-row items-center justify-between gap-4">
				<!-- 로고 및 버전 -->
				<div class="flex items-center gap-3">
					<span class="text-xl font-bold text-indigo-400">AI</span>
					<span class="text-lg font-semibold text-white">Lang</span>
					<span class="text-sm text-slate-500">{m.footer_version()}</span>
				</div>

				<!-- 링크들 -->
				<div class="flex flex-wrap items-center justify-center gap-4 md:gap-6">
					<!-- GitHub -->
					<a
						href="https://github.com/thruthesky/ailang"
						target="_blank"
						rel="noopener noreferrer"
						class="text-slate-400 hover:text-white transition-colors flex items-center gap-2"
					>
						<svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
							<path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
						</svg>
						{m.footer_github()}
					</a>
					<span class="text-slate-700">|</span>
					<!-- 커뮤니티 포럼 -->
					<a
						href="https://github.com/thruthesky/ailang/discussions"
						target="_blank"
						rel="noopener noreferrer"
						class="text-slate-400 hover:text-white transition-colors flex items-center gap-2"
					>
						<svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
							<path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z"/>
						</svg>
						{m.footer_discussions()}
					</a>
					<span class="text-slate-700">|</span>
					<!-- 라이선스 -->
					<span class="text-slate-400 text-sm">{m.footer_license()}</span>
				</div>
			</div>

			<!-- 하단: 연락처 및 저작권 -->
			<div class="flex flex-col md:flex-row items-center justify-between gap-2 pt-4 border-t border-slate-800">
				<!-- 연락처 -->
				<p class="text-slate-500 text-sm">
					{m.footer_contact()}: {m.footer_contact_name()} &lt;thruthesky@gmail.com&gt;
				</p>
				<!-- 저작권 -->
				<p class="text-slate-500 text-sm">
					{m.footer_copyright()}
				</p>
			</div>
		</div>
	</div>
</footer>
