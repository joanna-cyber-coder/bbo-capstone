Part 2: Model Card for the BBO Optimisation Approach

Model Overview

Approach Name: Sequential Coordinate Bisection with Contextual Recovery (SCB-CR)

Type: Derivative-Free Local Optimization / Hybrid Exploration-Exploitation Algorithm

Version: 2.0 (Pivoted Framework)

Intended Use

This approach is purpose-built for maximizing complex, expensive multi-dimensional black-box functions. It is ideal for local fine-tuning where you have high-quality baseline points and need to squeeze out peak performance under a highly restricted evaluation budget.

Do not use this algorithm on landscapes that are highly jagged, discontinuous, or contain sharp, needle-like isolated peaks. Because it searches axis by axis, it will completely step over great global peaks if they are isolated in flat, low-value terrain. Avoid it for parallel computing too, since its logic is strictly sequential.

Optimization Details (Strategy & Evolution)

My strategy completely transformed over the ten weeks as I adapted to the quirks of each black-box landscape.

Weeks 1–5 (Local Coordinate Ascent): I tweaked individual coordinate axes one at a time, moving outward from the baseline points. If a change improved the score, I kept moving that way and cut the step size in half (bisection) to zero in on the peak. If the output score dropped, I turned around.

Weeks 6–8 (The Stagnation Trap): A major weakness emerged. While simpler, lower-dimensional spaces like Function 5 (chemical yield) converged perfectly, high-dimensional spaces like Functions 7 and 8 (6D and 8D) completely flattened out and got stuck on low-value plateaus.

Weeks 9–10 (The Baseline Recovery Pivot): I audited the full dataset history and realized my local optimization path was trapped by over-confidence in a bad neighborhood. In Week 9, I made a massive macro-leap across the search space, abandoning the local tracks for Functions 7 and 8 entirely. I jumped straight back to the coordinates of the highest initial sample benchmarks (Index 6 and 14). This pivot instantly paid off, recovering the true global peaks (1.3649 and 9.5984) just in time for high-resolution refinement in Week 10.

Performance Summary

Success was evaluated using the All-Time Maximum Score (Ymax) achieved by the end of Round 10:

Function 1 (2D Sparse Field): Climbed from a near-zero initial state to a final value of 1.043 x 10^-7.

Function 2 (2D Noisy Model): Secured a peak of 0.7373 in Week 2, shielding it from noise by rejecting worse subsequent steps.

Function 3 (3D Drug Discovery): Successfully minimized adverse reactions to log a peak maximization score of -0.0236.

Function 4 (4D Warehouse Placement): Demonstrated steady coordinate gains, climbing smoothly to hit -3.8206.

Function 5 (4D Chemical Yield): Flawlessly mapped the smooth, unimodal terrain to dial in a peak yield of 1258.72.

Function 6 (5D Cake Recipe): Unlocked a brand-new all-time high score in Week 9 (-0.6360) using multi-axis bisections.

Functions 7 & 8 (6D & 8D): Successfully recovered from sub-optimal valleys via the Week 9 pivot to hit their true global leaders at 1.3649 and 9.5984.

Assumptions and Limitations

The core assumption driving this strategy is local smoothness—the belief that nearby points in the search space produce similar outputs. The primary failure mode is getting trapped in local hills because wide-area exploration is too expensive on a tight 10-step budget.

Ethical Considerations & Card Clarity

Documenting every input vector, output response, and step-halving decision ensures this strategy is entirely transparent and reproducible. Another student could take my history and recreate identical coordinate tracks without guessing. In real-world tuning, this transparency ensures that failures can be audited, predicted, and safely corrected.

The current concise structure is sufficient; adding complex math jargon or bloated data tables would only obscure the card's core utility, which is clearly explaining when, why, and how the optimization approach succeeds or fails.
