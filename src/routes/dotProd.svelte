<section>
	<h2 class="mb-1.5 text-[38px] font-bold text-[#2f5bea]">Q2 · Dot Product</h2>
	<div class="card flex flex-wrap items-center gap-3">
		u = <span class="vec"><span>2</span><span>1</span><span>3</span></span>, v =
		<span class="vec"><span>1</span><span>−2</span><span>0</span></span>
	</div>
	<div class="card fragment">
		<span class="tag">a</span>u · v = (2)(1) + (1)(−2) + (3)(0)
		<div class="why">Why: dot product = multiply matching entries, then add the results.</div>
	</div>
	<div class="card fragment">
		= 2 − 2 + 0 = <span class="ans">0</span>
		<div class="why">
			Why: the positive and negative terms cancel exactly, and the third term is 0 because v has a 0
			there.
		</div>
	</div>
</section>

<section>
	<h2 class="mb-1.5 text-[38px] font-bold text-[#2f5bea]">Q2 · Lengths of the Vectors</h2>
	<div class="mb-5 text-2xl text-[#5b6679]">(b) Use ‖x‖ = √(x · x)</div>
	<div class="card fragment">
		‖u‖ = √(2² + 1² + 3²) = √(4+1+9) = <span class="ans">√14 ≈ 3.74</span>
		<div class="why">
			Why: same Pythagorean idea as Q1d, extended to 3 entries: square each, add, take the root.
		</div>
	</div>
	<div class="card fragment">
		‖v‖ = √(1² + (−2)² + 0²) = √(1+4+0) = <span class="ans">√5 ≈ 2.24</span>
		<div class="why">Why: the third entry is 0, so it adds nothing under the root.</div>
	</div>
</section>

<section>
	<h2 class="mb-1.5 text-[38px] font-bold text-[#2f5bea]">Q2 · Orthogonality</h2>
	<div class="mb-5 text-2xl text-[#5b6679]">
		(c) Two vectors are orthogonal exactly when u · v = 0
	</div>
	<div class="card fragment">
		We found u · v = 0
		<div class="why">Why: the test for perpendicular vectors is a dot product of exactly 0.</div>
	</div>
	<div class="card fragment">
		<span class="ans">∴ u and v are orthogonal</span> (they meet at 90°, cos θ = 0)
		<div class="why">
			Why: cos θ = (u · v) / (‖u‖‖v‖). A zero numerator means cos θ = 0, so θ = 90°.
		</div>
	</div>
	<div class="card fragment text-[26px] text-[#5b6679]">
		Check: cos θ = (u·v) / (‖u‖‖v‖) = 0 / (√14·√5) = 0 ✓
	</div>
</section>

<section>
	<h2 class="mb-1.5 text-[38px] font-bold text-[#2f5bea]">Q2 · Graph: u ⟂ v in 3D</h2>
	<div class="flex items-center gap-5">
		<svg
			viewBox="0 0 560 380"
			class="h-[380px] w-[560px] shrink-0 rounded-[14px] border border-[#d9deea] bg-[#f4f6fc]"
		>
			<line class="ax" x1="165" y1="260" x2="435" y2="260" />
			<line class="ax" x1="300" y1="340" x2="300" y2="60" />
			<line class="ax" x1="395" y1="192" x2="205" y2="328" />
			<text x="442" y="265" fill="currentColor" font-size="16">y</text>
			<text x="306" y="64" fill="currentColor" font-size="16">z</text>
			<text x="192" y="346" fill="currentColor" font-size="16">x</text>
			<path
				class="dr"
				pathLength="1"
				stroke="#2f5bea"
				d="M300 260L282 170"
				style="animation-delay:.3s"
			/>
			<polygon
				class="hd"
				fill="#2f5bea"
				points="0,0 -14,-6 -14,6"
				transform="translate(282 170) rotate(-101.3)"
				style="animation-delay:1.2s"
			/>
			<text class="gt hd" fill="#2f5bea" x="290" y="166" style="animation-delay:1.2s">u</text>
			<path
				class="dr"
				pathLength="1"
				stroke="#e8830c"
				d="M300 260L178.5 282.5"
				style="animation-delay:1.6s"
			/>
			<polygon
				class="hd"
				fill="#e8830c"
				points="0,0 -14,-6 -14,6"
				transform="translate(178.5 282.5) rotate(169.5)"
				style="animation-delay:2.5s"
			/>
			<text class="gt hd" fill="#e8830c" x="160" y="306" style="animation-delay:2.5s">v</text>
			<path
				class="hd"
				style="animation-delay:3s"
				fill="none"
				stroke="#1a8f5a"
				stroke-width="2.5"
				d="M297.3 246.5L279.1 249.9L281.8 263.4"
			/>
			<text class="gt hd" fill="#1a8f5a" x="236" y="242" style="animation-delay:3s">90°</text>
		</svg>
		<div class="text-[23px] leading-[1.7]">
			<div class="hd text-[#2f5bea]" style="animation-delay:1.2s"><b>u</b> = (2, 1, 3)</div>
			<div class="hd text-[#e8830c]" style="animation-delay:2.5s"><b>v</b> = (1, −2, 0)</div>
			<div class="hd text-[#1a8f5a]" style="animation-delay:3s">
				<b>u · v = 0</b> → right angle
			</div>
			<div class="hd text-[26px] text-[#5b6679]" style="animation-delay:3.4s">
				A flat drawing of a 3D picture bends angles, so it looks skewed. The dot product is what
				proves it is 90°.
			</div>
		</div>
	</div>
</section>

<style>
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
