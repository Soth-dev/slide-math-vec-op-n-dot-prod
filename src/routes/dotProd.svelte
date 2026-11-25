<script lang="ts">
	// Q2: 3D vectors (default u = (2, 1, 3), v = (1, -2, 0))
	let u2x = $state(2);
	let u2y = $state(1);
	let u2z = $state(3);
	let v2x = $state(1);
	let v2y = $state(-2);
	let v2z = $state(0);

	const q2Dot = $derived(u2x * v2x + u2y * v2y + u2z * v2z);
	const q2LenU = $derived(Math.hypot(u2x, u2y, u2z));
	const q2LenV = $derived(Math.hypot(v2x, v2y, v2z));
	const q2CosTheta = $derived(q2LenU > 0 && q2LenV > 0 ? q2Dot / (q2LenU * q2LenV) : 0);
	const q2AngleDeg = $derived(
		Math.round(((Math.acos(Math.max(-1, Math.min(1, q2CosTheta))) * 180) / Math.PI) * 10) / 10
	);
	let q1Touched = $state(false);
	let q2Touched = $state(false);

	function angleDeg(dx: number, dy: number) {
		return (Math.atan2(dy, dx) * 180) / Math.PI;
	}

	// Q2 3D projected SVG endpoints & arrowhead angles

	function resetQ2() {
		u2x = 2;
		u2y = 1;
		u2z = 3;
		v2x = 1;
		v2y = -2;
		v2z = 0;
		q2Touched = false;
	}
	// 3D camera rotation (radians)
	let camYaw = $state(0.65);
	let camPitch = $state(0.35);
	let dragging3D = $state(false);
	let lastPointer = { x: 0, y: 0 };
	let q2CamTouched = $state(false);

	function project3D(x: number, y: number, z: number) {
		// Rotate around Z (yaw)
		const cosY = Math.cos(camYaw);
		const sinY = Math.sin(camYaw);
		const x1 = x * cosY - y * sinY;
		const y1 = x * sinY + y * cosY;

		// Tilt vertically (pitch)
		const cosP = Math.cos(camPitch);
		const sinP = Math.sin(camPitch);
		const y2 = y1 * cosP - z * sinP;
		const z2 = y1 * sinP + z * cosP;

		// Map to your 560x380 SVG around (300, 255)
		const scale = 36;
		const sx = 300 + x1 * scale;
		const sy = 255 - z2 * scale + y2 * scale * 0.45;
		return { x: sx, y: sy };
	}

	function on3DPointerDown(e: PointerEvent) {
		e.stopPropagation();
		dragging3D = true;
		q2CamTouched = true;
		lastPointer = { x: e.clientX, y: e.clientY };
		(e.currentTarget as Element).setPointerCapture?.(e.pointerId);
	}

	function on3DPointerMove(e: PointerEvent) {
		if (!dragging3D) return;
		e.stopPropagation();
		const dx = e.clientX - lastPointer.x;
		const dy = e.clientY - lastPointer.y;
		lastPointer = { x: e.clientX, y: e.clientY };

		camYaw += dx * 0.012;
		camPitch = Math.max(-1.2, Math.min(1.2, camPitch + dy * 0.012));
	}

	function on3DPointerUp(e: PointerEvent) {
		if (!dragging3D) return;
		e.stopPropagation();
		dragging3D = false;
	}
	function on3DKeyDown(e: KeyboardEvent) {
		if (e.key === 'r' || e.key === 'R') {
			e.stopPropagation();
			camYaw = 0.65;
			camPitch = 0.35;
			q2CamTouched = false;
		}
	}

	const q2Origin = $derived(project3D(0, 0, 0));
	const q2AxisX = $derived(project3D(4.2, 0, 0));
	const q2AxisY = $derived(project3D(0, 4.2, 0));
	const q2AxisZ = $derived(project3D(0, 0, 4.2));

	const q2UTip = $derived(project3D(u2x, u2y, u2z));
	const q2VTip = $derived(project3D(v2x, v2y, v2z));

	const q2U = $derived({
		x: q2UTip.x,
		y: q2UTip.y,
		deg: angleDeg(q2UTip.x - q2Origin.x, q2UTip.y - q2Origin.y)
	});

	const q2V = $derived({
		x: q2VTip.x,
		y: q2VTip.y,
		deg: angleDeg(q2VTip.x - q2Origin.x, q2VTip.y - q2Origin.y)
	});
</script>

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
	<div class="flex flex-col items-start gap-4 md:flex-row md:items-center md:gap-5">
		<button
			type="button"
			aria-label="Interactive 3D vector graph for u and v. Drag to rotate, press R to reset."
			onpointerdown={on3DPointerDown}
			onpointermove={on3DPointerMove}
			onpointerup={on3DPointerUp}
			onpointercancel={on3DPointerUp}
			onkeydown={on3DKeyDown}
			onclick={(e) => e.stopPropagation()}
			class="aspect-[560/380] max-h-[52vh] w-full max-w-[540px] shrink-0 cursor-grab touch-none overflow-hidden rounded-[14px] border border-[#d9deea] bg-[#f4f6fc] p-0 text-left focus:outline-none active:cursor-grabbing md:max-h-[360px] md:w-auto md:flex-1"
		>
			<svg
				viewBox="0 0 560 380"
				class:no-anim={q2Touched || q2CamTouched}
				class="block h-full w-full"
			>
				<!-- Dynamic 3D Axes -->
				<line class="ax" x1={q2Origin.x} y1={q2Origin.y} x2={q2AxisX.x} y2={q2AxisX.y} />
				<line class="ax" x1={q2Origin.x} y1={q2Origin.y} x2={q2AxisY.x} y2={q2AxisY.y} />
				<line class="ax" x1={q2Origin.x} y1={q2Origin.y} x2={q2AxisZ.x} y2={q2AxisZ.y} />
				<text x={q2AxisX.x + 6} y={q2AxisX.y + 6} fill="currentColor" font-size="15">x</text>
				<text x={q2AxisY.x + 6} y={q2AxisY.y + 6} fill="currentColor" font-size="15">y</text>
				<text x={q2AxisZ.x + 6} y={q2AxisZ.y - 4} fill="currentColor" font-size="15">z</text>

				<!-- u -->
				<path
					class="dr"
					pathLength="1"
					stroke="#2f5bea"
					d="M{q2Origin.x} {q2Origin.y}L{q2U.x} {q2U.y}"
					style="animation-delay:.3s"
				/>
				<polygon
					class="hd"
					fill="#2f5bea"
					points="0,0 -14,-6 -14,6"
					transform="translate({q2U.x} {q2U.y}) rotate({q2U.deg})"
					style="animation-delay:1.2s"
				/>
				<text class="gt hd" fill="#2f5bea" x={q2U.x + 8} y={q2U.y - 4} style="animation-delay:1.2s">
					u
				</text>

				<!-- v -->
				<path
					class="dr"
					pathLength="1"
					stroke="#e8830c"
					d="M{q2Origin.x} {q2Origin.y}L{q2V.x} {q2V.y}"
					style="animation-delay:1.6s"
				/>
				<polygon
					class="hd"
					fill="#e8830c"
					points="0,0 -14,-6 -14,6"
					transform="translate({q2V.x} {q2V.y}) rotate({q2V.deg})"
					style="animation-delay:2.5s"
				/>
				<text
					class="gt hd"
					fill="#e8830c"
					x={q2V.x - 18}
					y={q2V.y + 22}
					style="animation-delay:2.5s"
				>
					v
				</text>

				<!-- 90° Right-Angle Marker (appears whenever u · v = 0) -->
				{#if q2Dot === 0 && q2LenU > 0 && q2LenV > 0}
					{@const uStep = { x: (q2U.x - q2Origin.x) * 0.16, y: (q2U.y - q2Origin.y) * 0.16 }}
					{@const vStep = { x: (q2V.x - q2Origin.x) * 0.16, y: (q2V.y - q2Origin.y) * 0.16 }}
					<path
						class="hd"
						style="animation-delay:3s"
						fill="none"
						stroke="#1a8f5a"
						stroke-width="2.5"
						d="M{q2Origin.x + uStep.x} {q2Origin.y + uStep.y}L{q2Origin.x +
							uStep.x +
							vStep.x} {q2Origin.y + uStep.y + vStep.y}L{q2Origin.x + vStep.x} {q2Origin.y +
							vStep.y}"
					/>
					<text
						class="gt hd"
						fill="#1a8f5a"
						x={q2Origin.x + (uStep.x + vStep.x) * 1.9 - 14}
						y={q2Origin.y + (uStep.y + vStep.y) * 1.9}
						style="animation-delay:3s"
					>
						90°
					</text>
				{/if}
			</svg>
		</button>

		<!-- Sliders & Live Dot Product Readout -->
		<div
			class="w-full max-w-[300px] space-y-1.5 rounded-xl border border-[#d9deea] bg-[#f4f6fc] p-3 text-sm"
		>
			<div class="flex items-center justify-between font-bold text-[#2f5bea]">
				<span>u = ({u2x}, {u2y}, {u2z})</span>
				<button
					type="button"
					onclick={(e) => {
						e.stopPropagation();
						resetQ2();
					}}
					class="cursor-pointer rounded border border-[#d9deea] bg-white px-2 py-0.5 text-xs text-[#1b2333]"
				>
					Reset
				</button>
			</div>
			<label class="flex items-center justify-between gap-2">
				<span>uₓ</span>
				<input
					type="range"
					min="-4"
					max="4"
					step="1"
					bind:value={u2x}
					onclick={(e) => e.stopPropagation()}
					oninput={() => (q2Touched = true)}
					class="w-36"
				/>
			</label>
			<label class="flex items-center justify-between gap-2">
				<span>uᵧ</span>
				<input
					type="range"
					min="-4"
					max="4"
					step="1"
					bind:value={u2y}
					onclick={(e) => e.stopPropagation()}
					oninput={() => (q2Touched = true)}
					class="w-36"
				/>
			</label>
			<label class="flex items-center justify-between gap-2">
				<span class="leading-none">
					u<sub class="align-baseline text-[0.72em] leading-none">z</sub>
				</span>
				<input
					type="range"
					min="-4"
					max="4"
					step="1"
					bind:value={u2z}
					oninput={() => (q2Touched = true)}
					class="w-36"
				/>
			</label>

			<div class="pt-1 font-bold text-[#e8830c]">v = ({v2x}, {v2y}, {v2z})</div>
			<label class="flex items-center justify-between gap-2">
				<span>vₓ</span>
				<input
					type="range"
					min="-4"
					max="4"
					step="1"
					bind:value={v2x}
					oninput={() => (q2Touched = true)}
					class="w-36"
				/>
			</label>
			<label class="flex items-center justify-between gap-2">
				<span>vᵧ</span>
				<input
					type="range"
					min="-4"
					max="4"
					step="1"
					bind:value={v2y}
					oninput={() => (q2Touched = true)}
					class="w-36"
				/>
			</label>
			<label class="flex items-center justify-between gap-2">
				<span class="leading-none">
					u<sub class="align-baseline text-[0.72em] leading-none">z</sub>
				</span>
				<input
					type="range"
					min="-4"
					max="4"
					step="1"
					bind:value={v2z}
					oninput={() => (q2Touched = true)}
					class="w-36"
				/>
			</label>

			<div class="border-t border-[#d9deea] pt-2 leading-relaxed">
				<div class="font-bold text-[#1a8f5a]">
					u · v = {q2Dot}
					{q2Dot === 0 ? '(⟂ 90° orthogonal)' : `(θ ≈ ${q2AngleDeg}°)`}
				</div>
				<div class="text-xs text-[#5b6679]">
					‖u‖ = {q2LenU.toFixed(2)}, ‖v‖ = {q2LenV.toFixed(2)}
				</div>
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
