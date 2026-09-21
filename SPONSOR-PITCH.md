# Sponsoring VybFly — embiggenating the fly

**Target: M15, the 100× connectome (~14 million neurons).** It is the last unclimbed
rung on the project's own ladder, and the only milestone the README records as
`gated, not attempted` — blocked on vectorizing sibling-edge placement first.

Everything below is derived from VybFly's *own measured data*, not guesswork. The
arithmetic is shown so you can attack it.

---

## What already works

M0 through M14 are **done**. That matters for a funding ask, because you're not
paying for someone to build a thing from scratch — you're paying for the next rung
on a ladder that demonstrably holds:

| milestone | state |
|---|---|
| M0 canonical FlyWire graph + published-value gate | done — 11/11 required checks |
| M1 whole-connectome LIF baseline | done — dense and sparse agree exactly |
| M2 Vyb discrete-event engine | done — 4/4 replications match the reference |
| M3 Vyb GPU kernels | done — tick-for-tick agreement with the CPU reference |
| M4 energy instrumentation | done — GPU device power measured |
| M5–M8 geometry / downscale / upscale / closure | done |
| M9 dynamic validation of the replicas | done — 85–95% active-set overlap |
| M11–M14 learning, capability, energy, capability-per-watt | done — incl. the negative-control result |
| **M15 100× graph (~14M neurons)** | **gated, not attempted** |

Measured results standing behind that table:

- **438 → 2,022 J** across the 1× → 10× ladder (GPU device energy)
- **cost per spike falling 8.9 → 4.2 µJ** — the device stops being idle-bound
- 85–95% active-set overlap on dynamic validation
- a negative-control result that goes against the obvious guess

## What M15 buys

The 100× graph is where the project's central question gets its hardest test. The
paper asks whether you can make the map bigger and have it still work — the same
kind of wiring, the same signal spread, the same abilities. At 10×, on 1.4M
neurons, the answer is largely yes. At 100×, on ~14M, the open questions are:

- does the geometric growth law keep degree and mean connection strength bounded
  at the top of the range, or does it finally break?
- does cost per spike keep *falling* (the sub-linear edge that makes the GPU
  interesting), or does it turn over?
- does capability per watt hold, or collapse?

None of that is answerable without actually running it.

## What it costs — and the honest surprise

**The electricity is free. The GPU-hours are cheap. The engineering is the cost.**

That is what the numbers say, and it's worth stating plainly rather than dressing
up a small number as a big one.

**Energy.** Fitting the measured ladder (`J = 372.4 · S^0.669`, from 437.6 J at 1×
to 2,021.6 J at 10×) predicts about **8,100 J** for a comparable 100× payload —
**0.0023 kWh**. Run the whole campaign's iterations and it's on the order of
**0.04 kWh**, roughly **one cent** of electricity. Energy is not the constraint. It
never was; that is itself one of the project's findings.

**GPU-hours.** The measured GPU rate is **1.251 wall-seconds per bio-second** at
139,255 neurons (42 bio-seconds in 52.5 wall-seconds, RTX 3090). Scaling wall time
*linearly* with neuron count — a deliberately pessimistic upper bound, since work
per neuron need not grow linearly — gives:

| work unit at 100× (upper bound) | GPU-hours |
|---|---|
| 1 bio-second | 0.035 |
| 1 bio-minute | 2.1 |
| 1 bio-hour | 125.1 |
| **one 10-bio-minute validation run** | **20.9** |
| × 4 replications (the project's own M2 standard) | 83.4 |
| + development and iteration (15×, for debug cycles, failed attempts, profiling) | 1,251 |
| **total** | **≈1,334** |

**Dollars.** At community cloud rates for an RTX 3090-class GPU:

| rate | campaign cost |
|---|---|
| $0.35/GPU-hr | **≈$467** |
| $0.50/GPU-hr | **≈$667** |
| $0.80/GPU-hr | **≈$1,068** |

### Why the honest answer is "a few hundred dollars"

Because the thing blocking M15 is not compute — it's the **vectorization work**.
The README states M15 needs sibling-edge placement vectorized, plus node
subdivision extended to 100×. That is engineering, and engineering is paid in
time, not in GPU-hours. The GPU budget above is dominated by the *development*
term (15×), not by the science run (20.9 GPU-hours).

So a sponsorship is really buying: **a few hundred dollars of cloud GPU time so
the engineering doesn't have to pause whenever a debug cycle needs a big run.**

## What sponsorship would fund

1. **Cloud GPU budget** — ~$500–1,000 of RTX 3090-class time, covering M15's
   development iterations and the final 4×-replicated validation runs.
2. **Vectorizing sibling-edge placement** — the blocking dependency for 100×.
3. **Node subdivision at 100×** — the scale extension the current tests stop short of
   (they pass at 2× and 5×).
4. **The write-up** — M15's results folded into the paper, including the energy and
   capability-per-watt curves extended to 14M neurons.

## What sponsorship is *not*

Being straight about this is part of the pitch:

- **Not a salary.** This isn't someone quitting a job; it's a compute line item on
  work already in progress.
- **Not a promise M15 succeeds.** The project has a negative-control result in its
  own table. If the growth law breaks at 100×, that is a *finding*, and it gets
  reported as one. The metric is deliberately defined so a miss is visible rather
  than quietly absorbed.
- **Not conflating measurement with model.** The paper keeps hardware measurement and the
  biological-equivalent model in **strictly separate tracks** (§17) and never mixes
  them. Sponsoring keeps that separation intact.

## How to verify any of this

Everything above is reproducible from the repo:

```bash
gh repo clone rickenator/VybFly
python3 -c "import json;d=json.load(open('results/energy/curves.json'));print(d['per_scale'])"
```

- measured ladder: `results/energy/curves.json` → `per_scale[<scale>].hardware.gpu_joules`
- measured GPU rate: `results/energy/hardware_energy.json` → `workload_gpu` (52.54 wall-s, 42.0 bio-s)
- blocker: `docs/ROADMAP.md` (M15 row; sibling-edge placement, node subdivision 2×–100×)
- milestone table: `README.md` → Status

The paper: **https://vybfly-paper-relay.aniviza.workers.dev/paper.pdf**

## Tiers (suggested)

| tier | amount | what it maps to |
|---|---|---|
| Rung | $25 | one bio-hour's worth of 100× GPU time (125 GPU-hr upper bound) |
| Replication | $100 | one of the four validation replications, in full |
| Milestone | $500 | the M15 cloud budget at community rates |
| Embiggenator | $1,000+ | the full campaign, development iterations included |

Named credit for sponsors at the Milestone tier and above, unless you prefer
otherwise.

---

*Figures derived from VybFly's measured energy and timing data on an RTX 3090 and
a single-process CPU reference. Scaling assumptions are stated where used; the
linear-in-N wall-time bound is deliberately pessimistic.*
