<script lang="ts">
	// 루트 레이아웃 컴포넌트
	// 네비게이션과 푸터를 포함한 전체 페이지 구조를 정의합니다
	import './layout.css';
	import { m } from '$lib/paraglide/messages.js';
	import Navigation from '$lib/components/Navigation.svelte';
	import Footer from '$lib/components/Footer.svelte';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" type="image/png" href="/favicon.png" />
	<title>{m.site_title()}</title>
	<meta name="description" content={m.site_description()} />
	<!-- Open Graph 메타 태그 -->
	<meta property="og:title" content={m.site_title()} />
	<meta property="og:description" content={m.site_description()} />
	<meta property="og:type" content="website" />
	<meta property="og:url" content="https://ailang.dev" />
</svelte:head>

<!-- 전체 페이지 컨테이너 - 다크 테마 -->
<div class="min-h-screen flex flex-col bg-slate-900 text-slate-100">
	<!-- 상단 네비게이션 -->
	<Navigation />

	<!-- 메인 콘텐츠 영역 -->
	<main class="flex-1">
		{@render children()}
	</main>

	<!-- 하단 푸터 -->
	<Footer />
</div>
