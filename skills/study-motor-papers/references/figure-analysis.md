# Figure interpretation protocol

## Contents

1. Evidence order
2. Required Fig block
3. Plot-specific checks
4. Block diagrams and schematics
5. Motor-control interpretation checks
6. Common failure modes

## 1. Evidence order

Interpret each figure from these sources in order:

1. the actual pixels at readable resolution;
2. axes, legends, labels, annotations, and panel lettering;
3. the official caption;
4. nearby paragraphs and formula references;
5. methods and experimental conditions elsewhere in the paper;
6. domain reasoning.

When sources conflict, report the conflict. Do not let domain expectations override visible data.

## 2. Required Fig block

Place this block immediately under every figure after its translated caption:

### Fig X 图解

**这张图在展示什么**

State the object, variables, experiment/simulation condition, and each panel's role.

**先这样读图**

Explain axes and units, then legend/colors/line styles/markers, then the intended comparison or event sequence. Cover every panel `(a)`, `(b)`, and so on.

**能直接观察到的现象**

List only visible patterns: direction, magnitude, timing, phase, bandwidth, overshoot, steady-state error, ripple, slope, saturation, separation between curves, and transitions.

**作者用它支持什么结论**

Connect the figure to the nearby claim and quote no more source text than necessary.

**我的理解**

Explain the physical or control-theoretic mechanism. Connect to the relevant equation or block. Label the explanation as high-, medium-, or low-confidence.

**不能由此图单独推出什么**

Identify missing baselines, unreported conditions, scale limitations, confounding factors, or causal claims that exceed the evidence.

**容易误读的地方**

Explain ambiguous scales, normalized quantities, sign conventions, offset curves, panel-dependent legends, electrical/mechanical frequencies, filtered/raw signals, and visually small but quantitatively important differences.

Omit a heading only when genuinely irrelevant; never omit panel coverage or conclusion boundaries.

## 3. Plot-specific checks

For time-domain plots, inspect:

- trigger or event time;
- delay, rise/settling time, overshoot, oscillation, and steady-state error;
- whether traces use different axes or offsets;
- control saturation, current/voltage limits, and sampling/filter delay;
- whether the shown interval is long enough to support a stability claim.

For Bode/frequency plots, inspect:

- Hz versus rad/s and electrical versus mechanical frequency;
- magnitude units and phase wrapping convention;
- poles, zeros, corners, resonance/notch, asymptotic slopes, and phase limits;
- whether curves are theory, simulation, identification, or measurement;
- whether a claimed bandwidth follows the paper's stated definition.

For vector, trajectory, and dq/alpha-beta plots, inspect:

- frame orientation, rotation direction, zero-angle convention, and sign convention;
- scaling equality between axes;
- commanded, estimated, measured, and true quantities;
- whether an apparent phase error is a coordinate or plotting artifact.

For bar charts and parameter sweeps, inspect baselines, normalization, uncertainty/error bars, sample size, and whether only selected operating points are shown.

## 4. Block diagrams and schematics

- Trace signal direction and name each input, state, disturbance, and output.
- Expand summing-junction signs and feedback polarity.
- Map each block to its formula and distinguish implementation from conceptual grouping.
- Identify coordinate frames and sample/update rates where stated.
- Explain cross-coupling paths, feedforward paths, filters, delays, limiters, switching logic, and initialization.
- Do not assume an unlabeled block's transfer function.

## 5. Motor-control interpretation checks

Check especially for:

- phase versus line voltage/current and peak versus RMS quantities;
- mechanical speed, electrical speed, and pole-pair conversion;
- actual, reference, estimated, and observer-internal signals;
- rotor, stator, synchronous, alpha-beta, and dq frames;
- voltage-model versus current-model contributions;
- resistance and inductance parameter mismatch;
- inverter nonlinearity, dead time, saturation, sampling, filtering, and PWM effects;
- open-loop startup, convergence interval, handover, and closed-loop results;
- whether low-speed claims are supported by signal-to-noise ratio and load conditions;
- whether a controller and an observer are tested together, making attribution ambiguous.

## 6. Common failure modes

Never:

- infer red/green/black trace meanings without reading the legend;
- describe only the trend while ignoring units, panel differences, or test conditions;
- treat simulation traces as experimental validation;
- infer causality from coincident traces alone;
- call a filtered signal more accurate merely because it is smoother;
- read log-axis spacing as linear;
- overlook clipped axes, normalized amplitude, dual y-axes, or phase wrapping;
- treat an author's caption as proof when the visible curve does not clearly support it.

If a figure is unreadable, request a higher-resolution page or crop and state exactly which labels or curves remain unresolved.
