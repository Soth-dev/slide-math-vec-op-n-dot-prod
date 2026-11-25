<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import Reveal, { type RevealApi } from 'reveal.js';
	import 'reveal.js/reveal.css';
	import 'reveal.js/theme/white.css';
	import VecOp from './vecOp.svelte';
	import DotProd from './dotProd.svelte';

	let deckEl: HTMLDivElement;
	let deck: RevealApi | null = null;

	onMount(async () => {
		deck = new Reveal(deckEl, {
			hash: false, // avoids conflict with SvelteKit's hash router
			controls: true,
			progress: true,
			center: true,
			transition: 'slide',
			touch: true,
			width: 960,
			height: 640,
			keyboard: true,
			loop: false,
			margin: 0.05
		});
		await deck.initialize();
	});

	onDestroy(() => {
		deck?.destroy();
	});
</script>

<div class="reveal h-full w-full" bind:this={deckEl}>
	<div class="slides text-left">
		<section>
			<div class="mb-5 text-2xl text-[#5b6679]">CAMTECH University · Faculty of Engineering</div>
			<h1 class="mb-3 text-[52px] leading-[1.15] font-bold">Vectors &amp; the Dot Product</h1>
			<div class="mb-5 text-2xl text-[#5b6679]">
				FECO101 Mathematics for Engineering I — Assignment 1, Questions 1 &amp; 2
			</div>
			<div class="text-[26px] text-[#5b6679]">Press → or tap Next to begin</div>
		</section>
		<VecOp />
		<DotProd />
		<section class="text-center">
			<h1 class="mb-3 text-[52px] leading-[1.15] font-bold">Thank You!</h1>
			<div class="mb-5 text-2xl text-[#5b6679]">Any questions?</div>
			<div class="card">u · v = 0 ⇒ u ⟂ v</div>
			<div class="text-[26px] text-[#5b6679]">
				FECO101 · Mathematics for Engineering I · CAMTECH University
			</div>
		</section>
	</div>
</div>

<!--<div
	class="fixed right-4 z-9 flex gap-2"
	style="bottom: calc(14px + env(safe-area-inset-bottom, 0px));"
>
	<button
		type="button"
		id="p"
		onclick={() => deck?.prev()}
		class="cursor-pointer rounded-[10px] border border-[#d9deea] bg-[#f4f6fc] px-4 py-2 text-[18px] text-[#1b2333] transition-transform duration-150 active:scale-[0.92]"
	>
		← Prev
	</button>
	<button
		type="button"
		id="n"
		onclick={() => deck?.next()}
		class="cursor-pointer rounded-[10px] border border-[#d9deea] bg-[#f4f6fc] px-4 py-2 text-[18px] text-[#1b2333] transition-transform duration-150 active:scale-[0.92]"
	>
		Next →
	</button>
</div>-->

<style>
	:global(html, body) {
		height: 100%;
		margin: 0;
		padding: 0;
		overflow: hidden;
		background: #ffffff;
		color: #1b2333;
	}

	:global(.reveal) {
		position: relative;
		width: 100vw;
		height: 100vh;
		overflow: hidden;
	}

	:global(.reveal .slides) {
		position: absolute;
		top: 50%;
		left: 50%;
		text-align: left;
		pointer-events: none;
	}

	:global(.reveal .slides > section) {
		position: absolute;
		left: 0;
		top: 0;
		width: 100%;
		box-sizing: border-box;
		padding: 0 40px;
		pointer-events: auto;
	}

	:global(.reveal .slides > section:not(.present)) {
		display: none !important;
	}

	:global(.reveal .fragment) {
		opacity: 0;
		visibility: hidden;
		transform: translateY(54px) scale(0.8);
		transition:
			opacity 0.5s ease,
			transform 0.5s cubic-bezier(0.2, 0.8, 0.2, 1);
	}

	:global(.reveal .fragment.visible) {
		opacity: 1;
		visibility: inherit;
		transform: none;
	}

	@layer components {
		.card {
			background: #f4f6fc;
			border: 1px solid #d9deea;
			border-radius: 14px;
			padding: 12px 22px;
			margin: 9px 0;
			font-size: 27px;
		}
	}

	:global(.reveal .slides > section.present) {
		animation: slin 0.6s cubic-bezier(0.2, 0.8, 0.2, 1);
	}
	:global(.reveal .slides > section.present h1),
	:global(.reveal .slides > section.present h2) {
		animation: drop 1s cubic-bezier(0.2, 0.8, 0.2, 1);
	}
	:global(.fragment.visible .ans) {
		animation: pop 0.6s 0.15s both;
	}

	@keyframes slin {
		from {
			opacity: 0;
			transform: translateX(600px);
		}
		to {
			opacity: 1;
			transform: none;
		}
	}
	@keyframes drop {
		from {
			opacity: 0;
			transform: translateY(-34px);
		}
		to {
			opacity: 1;
			transform: none;
		}
	}
	@keyframes pop {
		0% {
			transform: scale(0.8);
		}
		60% {
			transform: scale(1.12);
		}
		100% {
			transform: scale(1);
		}
	}

	@keyframes fin {
		to {
			opacity: 1;
		}
	}

	@media (prefers-reduced-motion: reduce) {
		:global(.reveal *) {
			animation: none !important;
			transition: none !important;
		}
	}
</style>
