# Sponsorship

**VybFly is fundable via GitHub Sponsors.** The campaigns are scoped to the next
unclimbed milestone, and every ask is backed by the project's own measured data.

## The target: M15 — the 100× connectome (~14M neurons)

The last rung on the project's ladder, and the only milestone the README records as
`gated, not attempted` (blocked on vectorizing sibling-edge placement first).

## The honest cost picture

Read the full pitch: **[SPONSOR-PITCH.md](SPONSOR-PITCH.md)**

Short version, derived from `results/energy/*.json` in the VybFly repo:

| item | figure |
|---|---|
| measured ladder (GPU) | 438 J @ 1× → 2,022 J @ 10× |
| measured GPU rate | 1.251 wall-s per bio-s (139,255 neurons, RTX 3090) |
| one 10-bio-min validation run @ 100× (upper bound) | 20.9 GPU-hr |
| × 4 replications | 83.4 GPU-hr |
| development/iteration (15×) | 1,251 GPU-hr |
| **total** | **≈1,334 GPU-hr** |
| **dollars @ $0.35–0.80/GPU-hr** | **≈$467–$1,068** |
| **electricity for the whole campaign** | **≈0.04 kWh — about one cent** |

The surprise worth knowing: **energy is not the constraint.** A 100× payload is
predicted at ~8,100 J (0.0023 kWh). The real cost is engineering time blocked by
GPU-hour access, not electricity — which is itself one of the project's findings.

## Verify it yourself

```bash
gh repo clone rickenator/VybFly
python3 -c "import json;d=json.load(open('results/energy/curves.json'));print(d['per_scale'])"
```

The paper: https://vybfly-paper-relay.aniviza.workers.dev/paper.pdf
