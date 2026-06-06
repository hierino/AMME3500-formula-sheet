# AMME3500 Formula Sheet Review & Project Context

## Git Workflow (MANDATORY)
After **every edit** to any file in this project, always:
1. `git add <changed files>`
2. `git commit -m "<short description of change>"`
3. `git push`

Do this automatically without being asked. Never leave uncommitted changes.

---

## Project Overview
**Course:** AMME3500 System Dynamics and Control (University of Sydney)  
**Assessable Content:** Past exams (2022, 2023, 2024), lecture slides (Lec 1–12), tutorial questions & solutions (Weeks 2–11)  
**Key Deliverable:** A single-page, landscape, 3-column formula sheet (`AMME3500_FS.pdf` → now `AMME3500_FS_V2.pdf`)

---

## Formula Sheet Contents (22 Sections)

### Core Material Covered
1. **Dynamical Systems & State-Space** (§1–2): ODE ↔ state-space conversion, linearisation via Jacobian
2. **First/Second-Order Response** (§3–6): Time constants, poles, damping ratio ζ, overshoot/settling time specs
3. **Control Design** (§7–8): PID control, effect of zeros (min-phase vs RHP)
4. **State-Space Methods** (§9–11): Transfer function from SS, reachability, observability, Luenberger observer, separation principle
5. **Frequency-Domain** (§12–17): Bode plots, Nyquist criterion, stability margins, sensitivity functions S & T
6. **Practical Tuning** (§18): Ziegler–Nichols method
7. **Quick Refs** (§19–22): Block diagram algebra, exam tips, math toolbox, worked patterns

---

## Verification Against Exams

### 2024 Exam
- ✅ All 7 questions fully covered
- Worked patterns match exactly (Q1 first-order ID, Q2 PD design, Q4 observer pole placement)
- DC gain (new addition) helps interpret step-response features in Q2 & Q7

### 2023 Exam
- ✅ All 8 questions covered
- **New addition:** Forced sinusoidal response (§12) directly solves Q3c (undamped pendulum $\ddot x + \frac{g}{\ell}x = \sin\omega t$ → $X = \frac{1}{\omega_n^2-\omega^2}$, resonance caveat)
- Observer & reachability questions identical to 2024 structure

### 2022 Exam
- ✅ 21 quiz + analysis problems; all tools present
- **Uses:** State-space cascading (§19), separation principle (§11), sensitivity functions (§16), loop shaping (§16), PID vs state-feedback comparison (§20—newly expanded)
- Q17, Q18: Pole placement on non-canonical forms (direct coefficient matching, §10)
- Q16: Insulin/glucose step-response features rely on DC gain sign/magnitude

---

## Key Additions Made (Chat Feedback)

### 1. **DC Gain for Step Response** (§3)
```
x(∞) = G(0) · U  (for any stable G and step size U)
```
- **Why added:** Every exam has step-response final-value questions (2024 Q1c, Q2, Q16-insulin; 2022 Q10, Q16)
- **Insight:** Sign of G(0) tells direction; magnitude gives final value
- **Consistency:** Generalises the first-order result x∞ = u/a

### 2. **Forced Sinusoidal Response & Resonance** (§12)
```
For ẍ + ωₙ²x = sin ωt, try x = X sin ωt:
X = 1/(ωₙ² - ω²)  [real → phase 0°/180°, no lag]
X → ∞ as ω → ωₙ  [resonance in undamped case]
```
- **Why added:** 2023 Q3c explicitly asks students to derive this for a pendulum
- **Method:** Undetermined coefficients (match coefficients of sin ωt)
- **Physics:** Undamped system has no damping, so resonance blows up

### 3. **Reachable Canonical (Companion) Form** (§10)
```
For ⃛y + a₁ÿ + a₂ẏ + a₃y = u:
A = [-a₁  -a₂  -a₃]    B = [1]
    [ 1    0    0 ]        [0]
    [ 0    1    0 ]        [0]
Char. poly s³ + a₁s² + a₂s + a₃ read off top row.
```
- **Why added:** Lectures reference the form; exams use it implicitly
- **Usage in practice:** 2022 Q17 & 2024 Q4 solve via direct coefficient matching (doesn't require the transformation, but structure is useful)

### 4. **Separation Principle** (§11, expanded)
- Clarifies that K and L can be designed independently for reachable & observable systems
- CL poles = union of controller poles (eig A−BK) and observer poles (eig A−LC)
- Directly addresses 2022 Q14 (separation principle essay question)

### 5. **Loop-Shaping Why/How** (§16, expanded)
```
(i)   High gain / integrator at low ω → tracking + reject disturbance d (S ≈ 0)
(ii)  Low gain + steep roll-off at high ω → reject noise n (T ≈ 0)
(iii) Gentle slope (≈ −20dB/dec) near ωgc → keep phase margin
```
- Directly answers 2022 Q15 (motivation & procedure for loop shaping)

### 6. **Cascaded State-Space Systems** (§19)
```
S₁ → S₂ in series: Gᵢ = Cᵢ(sI−Aᵢ)⁻¹Bᵢ + Dᵢ for each
Gtot = G₂G₁  (multiply TFs — easier than building one big A)
```
- Addresses 2022 Q20 (cascade transfer function computation)

### 7. **PID vs State-Feedback Comparison** (§20)
- **PID:** Model-free, SISO, heuristic/robust, simple to tune, limited pole control
- **State-FB:** Needs accurate model + full state (or observer), MIMO, exact pole placement
- Directly prepares for 2022 Q11 (compare benefits & limitations)

---

## What Was NOT Added (& Why)

### ❌ Laplace Transform / Final Value Theorem
- **Course decision:** Lec 3 explicitly states "Why don't we use Laplace transform in this unit?"
- The course uses time-domain ODE solutions + $G(j\omega)$ + exponential input response ($Ue^{st}$)
- ✅ This approach is already fully on the sheet

### ❌ Integral-Action Augmented System Matrices
- Sheet covers the concept: $\dot q = Cx - \bar y$ (§11)
- Exam answers (2024 Q7c, 2022 Q21) ask "describe your approach" (prose), not write matrices
- Concept coverage is sufficient

### ❌ Observable Canonical Form
- Similar to reachable canonical: referenced but rarely needed for exams
- 2×2 SISO problems always use direct coefficient matching (already on sheet)

### ❌ Routh–Hurwitz Stability Criterion
- Course uses Nyquist (frequency domain) and pole location (time domain) instead
- No exam questions test Routh–Hurwitz

---

## Course Philosophy Notes

1. **No Laplace/FVT:** The course deliberately avoids transforms. All solutions are in time domain.
2. **Emphasis on understanding:** Exams mix "show every step" calculations with "describe your approach" essays (especially 2022 written section).
3. **SISO focus:** State-feedback and observer design use 2nd-order canonical examples; Nyquist & Bode are the main frequency-domain tools.
4. **Practical tuning:** Ziegler–Nichols and proportional feedback appear throughout; integral action for zero SS error.

---

## Usage in Claude Code Projects

This sheet is **complete & verified** against all three past exams. When working on AMME3500 problems:

- **For worked solutions:** Refer to §22 (Worked Patterns) — they match exam question structures exactly
- **For essay answers:** Use §16 (loop-shaping why/how), §11 (separation principle), §20 (PID vs state-FB) for conceptual framing
- **For pole placement:** Use §10 (coefficient matching) or §11 (observer pole design) — no need for canonical transformations in 2nd order
- **For frequency response:** §12–15 cover all Nyquist/Bode/margin calculations

---

## Files Referenced

- `AMME3500_FS_V2.pdf` — Final formula sheet (this version with all 7 additions)
- `AMME3500exam2024.pdf` + solutions (5 pages, 7 questions)
- `Exam2023.pdf` + solutions (6 pages, 8 questions)
- `Exam2022.pdf` (18 pages: 10 quiz + 11 written/analysis)
- `Lec1-12_AMME3500.pdf` (lecture slides, weeks 1–12)
- `Wk2-11_Tutorial_*.pdf` (tutorials & solutions)

---

## Quality Checks Performed

✅ 2024 exam: All 7 questions solvable with sheet formulas  
✅ 2023 exam: Q3c (sinusoidal forcing) now explicitly covered  
✅ 2022 exam: Q14 (separation), Q15 (loop-shaping), Q20 (cascaded SS), Q21 (integral) now well-supported  
✅ Math toolbox: All required algebra (complex numbers, partial fractions, 2×2 ops) present  
✅ No contradictions with course philosophy (no Laplace, no Routh–Hurwitz)  
✅ Canonical form structure matches Lec 7 examples  

---

**Last Updated:** June 2026  
**Confidence Level:** High — all additions verified against lecture content & all three past exams
