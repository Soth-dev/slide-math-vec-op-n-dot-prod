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
	<div class="flex items-center gap-5">
		<svg
			viewBox="0 0 560 380"
			class="h-[380px] w-[560px] shrink-0 rounded-[14px] border border-[#d9deea] bg-[#f4f6fc]"
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
			<line class="dash hd" style="animation-delay:2.4s" x1="280" y1="115" x2="480" y2="165" />
			<line class="dash hd" style="animation-delay:2.4s" x1="380" y1="315" x2="480" y2="165" />
			<line class="dash hd" style="animation-delay:4.6s" x1="380" y1="315" x2="280" y2="115" />
			<path
				class="dr"
				pathLength="1"
				stroke="#2f5bea"
				d="M180 265L280 115"
				style="animation-delay:.2s"
			/>
			<polygon
				class="hd"
				fill="#2f5bea"
				points="0,0 -14,-6 -14,6"
				transform="translate(280 115) rotate(-56.3)"
				style="animation-delay:1.1s"
			/>
			<text class="gt hd" fill="#2f5bea" x="288" y="112" style="animation-delay:1.1s">u</text>
			<path
				class="dr"
				pathLength="1"
				stroke="#e8830c"
				d="M180 265L380 315"
				style="animation-delay:1.4s"
			/>
			<polygon
				class="hd"
				fill="#e8830c"
				points="0,0 -14,-6 -14,6"
				transform="translate(380 315) rotate(14.04)"
				style="animation-delay:2.3s"
			/>
			<text class="gt hd" fill="#e8830c" x="386" y="334" style="animation-delay:2.3s">v</text>
			<path
				class="dr"
				pathLength="1"
				stroke="#1a8f5a"
				d="M180 265L480 165"
				style="animation-delay:2.6s"
			/>
			<polygon
				class="hd"
				fill="#1a8f5a"
				points="0,0 -14,-6 -14,6"
				transform="translate(480 165) rotate(-18.43)"
				style="animation-delay:3.5s"
			/>
			<text class="gt hd" fill="#1a8f5a" x="470" y="150" style="animation-delay:3.5s">u+v</text>
			<path
				class="dr"
				pathLength="1"
				stroke="#a23fd1"
				d="M180 265L80 65"
				style="animation-delay:3.8s"
			/>
			<polygon
				class="hd"
				fill="#a23fd1"
				points="0,0 -14,-6 -14,6"
				transform="translate(80 65) rotate(-116.57)"
				style="animation-delay:4.7s"
			/>
			<text class="gt hd" fill="#a23fd1" x="92" y="60" style="animation-delay:4.7s">u−v</text>
		</svg>
		<div class="text-[23px] leading-[1.7]">
			<div class="hd text-[#2f5bea]" style="animation-delay:1.1s"><b>u</b> = (2, 3)</div>
			<div class="hd text-[#e8830c]" style="animation-delay:2.3s"><b>v</b> = (4, −1)</div>
			<div class="hd text-[#1a8f5a]" style="animation-delay:3.5s">
				<b>u+v</b> = (6, 2)<br /><span class="text-[26px] text-[#5b6679]">
					diagonal of the parallelogram
				</span>
			</div>
			<div class="hd text-[#a23fd1]" style="animation-delay:4.7s">
				<b>u−v</b> = (−2, 4)<br /><span class="text-[26px] text-[#5b6679]">
					joins the tip of v to the tip of u
				</span>
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
