<script lang="ts">
	// Q1: 2D vectors (default u = (2, 3), v = (4, -1))
	let u1x = $state(2);
	let u1y = $state(3);
	let v1x = $state(4);
	let v1y = $state(-1);

	const q1Sum = $derived({ x: u1x + v1x, y: u1y + v1y });
	const q1Diff = $derived({ x: u1x - v1x, y: u1y - v1y });
	const q1LenU = $derived(Math.hypot(u1x, u1y));
	let q1Touched = $state(false);
	let q2Touched = $state(false);

	function angleDeg(dx: number, dy: number) {
		return (Math.atan2(dy, dx) * 180) / Math.PI;
	}

	// Q1 SVG endpoints & arrowhead angles
	const q1U = $derived({
		x: 180 + u1x * 50,
		y: 265 - u1y * 50,
		deg: angleDeg(u1x * 50, -u1y * 50)
	});
	const q1V = $derived({
		x: 180 + v1x * 50,
		y: 265 - v1y * 50,
		deg: angleDeg(v1x * 50, -v1y * 50)
	});
	const q1S = $derived({
		x: 180 + q1Sum.x * 50,
		y: 265 - q1Sum.y * 50,
		deg: angleDeg(q1Sum.x * 50, -q1Sum.y * 50)
	});
	const q1D = $derived({
		x: 180 + q1Diff.x * 50,
		y: 265 - q1Diff.y * 50,
		deg: angleDeg(q1Diff.x * 50, -q1Diff.y * 50)
	});

	function resetQ1() {
		u1x = 2;
		u1y = 3;
		v1x = 4;
		v1y = -1;
		q1Touched = false;
	}
</script>

<section>
	<h2 class="mb-1.5 text-[38px] font-bold text-[#2f5bea]">Q1 · Vector Operations</h2>
	<div class="mb-5 text-2xl text-[#5b6679]">Given u and v, compute (a) u + v and (b) u − v</div>
	<div class="card flex flex-wrap items-center gap-3">
		u = <span class="vec"><span>2</span><span>3</span></span>, v =
		<span class="vec"><span>4</span><span>−1</span></span>
	</div>
	<div class="card fragment">
		<span class="tag">a</span>u + v =
		<span class="vec"><span>2+4</span><span>3+(−1)</span></span>
		= <span class="vec ans"><span>6</span><span>2</span></span>
		<div class="why">Why: add vectors entry by entry — first with first, second with second.</div>
	</div>
	<div class="card fragment">
		<span class="tag">b</span>u − v =
		<span class="vec"><span>2−4</span><span>3−(−1)</span></span>
		= <span class="vec ans"><span>−2</span><span>4</span></span>
		<div class="why">
			Why: subtract entry by entry. Subtracting −1 is the same as adding 1, so 3 − (−1) = 4.
		</div>
	</div>
</section>

<section>
	<h2 class="mb-1.5 text-[38px] font-bold text-[#2f5bea]">Q1 · Scalar Multiples &amp; Length</h2>
	<div class="card">
		<span class="tag">c</span>3u − 2v
		<div class="why">
			Why: scale first (multiply every entry by the number), then subtract entry by entry. 3u = (6,
			9), 2v = (8, −2).
		</div>
	</div>
	<div class="card fragment flex flex-wrap items-center gap-3">
		<span class="vec"><span>6</span><span>9</span></span> −
		<span class="vec"><span>8</span><span>−2</span></span>
		= <span class="vec ans"><span>−2</span><span>11</span></span>
		<div class="why w-full">Why: 6 − 8 = −2 and 9 − (−2) = 11.</div>
	</div>
	<div class="card fragment">
		<span class="tag">d</span>‖u‖ = √(2² + 3²) = √(4 + 9) = <span class="ans">√13 ≈ 3.61</span>
		<div class="why">
			Why: u is the hypotenuse of a right triangle with legs 2 and 3, so length = √(sum of squares).
		</div>
	</div>
</section>

<section>
	<h2 class="mb-1.5 text-[38px] font-bold text-[#2f5bea]">Q1 · Graph of the Vectors</h2>
	<div class="flex flex-col items-start gap-4 md:flex-row md:items-center md:gap-5">
		<svg
			viewBox="0 0 560 380"
			class:no-anim={q1Touched}
			class="aspect-[560/380] max-h-[52vh] w-full max-w-[540px] shrink-0 rounded-[14px] border border-[#d9deea] bg-[#f4f6fc] md:max-h-[360px] md:w-auto md:flex-1"
		>
			<defs>
				<pattern id="g" width="50" height="50" patternUnits="userSpaceOnUse" x="30" y="15">
					<path d="M50 0H0V50" fill="none" class="gr" />
				</pattern>
			</defs>
			<rect x="30" y="15" width="500" height="350" fill="url(#g)" />
			<line class="ax" x1="30" y1="265" x2="530" y2="265" />
			<line class="ax" x1="180" y1="15" x2="180" y2="365" />
			<text x="518" y="284" fill="currentColor" font-size="16">x</text>
			<text x="188" y="28" fill="currentColor" font-size="16">y</text>

			<!-- Dashed parallelogram & difference lines -->
			<line
				class="dash hd"
				style="animation-delay:2.4s"
				x1={q1U.x}
				y1={q1U.y}
				x2={q1S.x}
				y2={q1S.y}
			/>
			<line
				class="dash hd"
				style="animation-delay:2.4s"
				x1={q1V.x}
				y1={q1V.y}
				x2={q1S.x}
				y2={q1S.y}
			/>
			<line
				class="dash hd"
				style="animation-delay:4.6s"
				x1={q1V.x}
				y1={q1V.y}
				x2={q1U.x}
				y2={q1U.y}
			/>

			<!-- u -->
			<path
				class="dr"
				pathLength="1"
				stroke="#2f5bea"
				d="M180 265L{q1U.x} {q1U.y}"
				style="animation-delay:.2s"
			/>
			<polygon
				class="hd"
				fill="#2f5bea"
				points="0,0 -14,-6 -14,6"
				transform="translate({q1U.x} {q1U.y}) rotate({q1U.deg})"
				style="animation-delay:1.1s"
			/>
			<text class="gt hd" fill="#2f5bea" x={q1U.x + 8} y={q1U.y - 3} style="animation-delay:1.1s">
				u
			</text>

			<!-- v -->
			<path
				class="dr"
				pathLength="1"
				stroke="#e8830c"
				d="M180 265L{q1V.x} {q1V.y}"
				style="animation-delay:1.4s"
			/>
			<polygon
				class="hd"
				fill="#e8830c"
				points="0,0 -14,-6 -14,6"
				transform="translate({q1V.x} {q1V.y}) rotate({q1V.deg})"
				style="animation-delay:2.3s"
			/>
			<text class="gt hd" fill="#e8830c" x={q1V.x + 6} y={q1V.y + 19} style="animation-delay:2.3s">
				v
			</text>

			<!-- u + v -->
			<path
				class="dr"
				pathLength="1"
				stroke="#1a8f5a"
				d="M180 265L{q1S.x} {q1S.y}"
				style="animation-delay:2.6s"
			/>
			<polygon
				class="hd"
				fill="#1a8f5a"
				points="0,0 -14,-6 -14,6"
				transform="translate({q1S.x} {q1S.y}) rotate({q1S.deg})"
				style="animation-delay:3.5s"
			/>
			<text class="gt hd" fill="#1a8f5a" x={q1S.x - 10} y={q1S.y - 15} style="animation-delay:3.5s">
				u+v
			</text>

			<!-- u - v -->
			<path
				class="dr"
				pathLength="1"
				stroke="#a23fd1"
				d="M180 265L{q1D.x} {q1D.y}"
				style="animation-delay:3.8s"
			/>
			<polygon
				class="hd"
				fill="#a23fd1"
				points="0,0 -14,-6 -14,6"
				transform="translate({q1D.x} {q1D.y}) rotate({q1D.deg})"
				style="animation-delay:4.7s"
			/>
			<text class="gt hd" fill="#a23fd1" x={q1D.x + 12} y={q1D.y - 5} style="animation-delay:4.7s">
				u−v
			</text>
		</svg>

		<!-- Sliders & Live Readout -->
		<div
			class="w-full max-w-[300px] space-y-2 rounded-xl border border-[#d9deea] bg-[#f4f6fc] p-3 text-base"
			onclick={(e) => e.stopPropagation()}
		>
			<div class="flex items-center justify-between font-bold text-[#2f5bea]">
				<span>u = ({u1x}, {u1y})</span>
				<button
					type="button"
					onclick={resetQ1}
					class="cursor-pointer rounded border border-[#d9deea] bg-white px-2 py-0.5 text-xs text-[#1b2333]"
				>
					Reset
				</button>
			</div>
			<label class="flex items-center justify-between gap-2 text-sm">
				<span>uₓ</span>
				<input
					type="range"
					min="-5"
					max="5"
					step="1"
					bind:value={u1x}
					oninput={() => (q1Touched = true)}
					class="w-40"
				/>
			</label>
			<label class="flex items-center justify-between gap-2 text-sm">
				<span>uᵧ</span>
				<input
					type="range"
					min="-4"
					max="4"
					step="1"
					bind:value={u1y}
					oninput={() => (q1Touched = true)}
					class="w-40"
				/>
			</label>

			<div class="pt-1 font-bold text-[#e8830c]">v = ({v1x}, {v1y})</div>
			<label class="flex items-center justify-between gap-2 text-sm">
				<span>vₓ</span>
				<input
					type="range"
					min="-5"
					max="5"
					step="1"
					bind:value={v1x}
					oninput={() => (q1Touched = true)}
					class="w-40"
				/>
			</label>
			<label class="flex items-center justify-between gap-2 text-sm">
				<span>vᵧ</span>
				<input
					type="range"
					min="-4"
					max="4"
					step="1"
					bind:value={v1y}
					oninput={() => (q1Touched = true)}
					class="w-40"
				/>
			</label>

			<div class="border-t border-[#d9deea] pt-2 text-sm leading-relaxed">
				<div class="font-semibold text-[#1a8f5a]">u + v = ({q1Sum.x}, {q1Sum.y})</div>
				<div class="font-semibold text-[#a23fd1]">u − v = ({q1Diff.x}, {q1Diff.y})</div>
				<div class="text-[#5b6679]">‖u‖ = {q1LenU.toFixed(2)}</div>
			</div>
		</div>
	</div>
</section>

<style>
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
		transform: translateY(24px) scale(0.97);
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
		.why {
			font-size: 20px;
			line-height: 1.35;
			color: #5b6679;
			font-weight: 400;
			border-left: 4px solid #2f5bea;
			padding: 4px 12px;
			margin-top: 8px;
		}
		.vec {
			display: inline-flex;
			flex-direction: column;
			align-items: center;
			padding: 0 10px;
			border-left: 2px solid currentColor;
			border-right: 2px solid currentColor;
			border-radius: 6px;
			line-height: 1.25;
			font-size: 0.85em;
			min-width: 1.4em;
		}
		.ans {
			color: #1a8f5a;
			font-weight: 700;
			display: inline-block;
		}
		.tag {
			display: inline-block;
			background: #2f5bea;
			color: #ffffff;
			border-radius: 8px;
			padding: 2px 12px;
			font-weight: 700;
			margin-right: 10px;
		}
	}

	:global(.reveal .slides > section.present) {
		animation: slin 0.6s cubic-bezier(0.2, 0.8, 0.2, 1);
	}
	:global(.reveal .slides > section.present h1),
	:global(.reveal .slides > section.present h2) {
		animation: drop 0.7s cubic-bezier(0.2, 0.8, 0.2, 1);
	}
	:global(.fragment.visible .ans) {
		animation: pop 0.6s 0.15s both;
	}

	@keyframes slin {
		from {
			opacity: 0;
			transform: translateX(60px);
		}
		to {
			opacity: 1;
			transform: none;
		}
	}
	@keyframes drop {
		from {
			opacity: 0;
			transform: translateY(-24px);
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

	.ax {
		stroke: #5b6679;
		stroke-width: 1.5;
	}
	.gr {
		stroke: #d9deea;
		stroke-width: 1;
	}
	.dr {
		stroke-dasharray: 1;
		stroke-dashoffset: 1;
		fill: none;
		stroke-width: 4;
		stroke-linecap: round;
	}
	:global(.present) .dr {
		animation: draw 1s ease forwards;
	}
	@keyframes draw {
		to {
			stroke-dashoffset: 0;
		}
	}
	.hd {
		opacity: 0;
	}
	:global(.present) .hd {
		animation: fin 0.4s ease forwards;
	}
	@keyframes fin {
		to {
			opacity: 1;
		}
	}
	.gt {
		font-size: 20px;
		font-weight: 700;
	}
	.dash {
		stroke: #5b6679;
		stroke-width: 2;
		stroke-dasharray: 6 5;
		fill: none;
	}

	@media (prefers-reduced-motion: reduce) {
		:global(.reveal *) {
			animation: none !important;
			transition: none !important;
		}
		.dr {
			stroke-dashoffset: 0 !important;
		}
		.hd {
			opacity: 1 !important;
		}
	}
</style>
