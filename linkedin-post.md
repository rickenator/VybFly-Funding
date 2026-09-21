I spent several months rebuilding a fruit-fly brain at 10x scale. The most interesting result was the one where nothing happened.

Here's the setup. In 2024, FlyWire mapped all 139,000 neurons and ~500 million synapses of an adult fruit fly — the first complete wiring diagram of a brain anyone has ever had.

So we took that map and asked: can you make it bigger and have it still work?

We grew it to 2x, 5x, and 10x — up to 1.4 million neurons and 27.8 million connections — then tested whether the enlarged versions still behave like brains: same wiring statistics, same signal spread, same abilities, and what it costs in energy.

Most of it held. Connectivity scaled cleanly (E ~ N^1.017, R²=0.999). Signals still spread. Memory capacity grew.

Then we ran the test that surprised us.

We took the fly's learning center — the mushroom body — and trained it on odor–reward association. It learned, going from chance to perfect in 58 trials.

Then we replaced the brain's *actual wiring* with a randomly shuffled version with identical statistics. Same neuron types, same connection counts, same degree distribution — just rewired randomly.

It learned exactly as well. +0.000 ± 0.000.

But here's what makes it a real result rather than a null one: when we froze plasticity, learning collapsed. Real wiring, frozen: 0.31 AUC. Shuffled wiring, frozen: 0.57. Same collapse either way.

What that tells us: the specific geometry of the connectome contributes nothing to this learning task. What matters is the *anatomy of the dopamine gating* — where the reward signal enters, and what it modulates. The wiring diagram is scaffolding; the gating structure is the machinery.

I think this is worth sharing because it constrains what "the connectome is special" can mean. A wiring diagram being complete doesn't make it sufficient. For this task, the work was in the architecture, not the topology.

Two things I'd flag honestly:

The capability curve is censored — our test grid ran out before the system did, so I can't tell you how far capacity actually grows. I'd rather say that than fit a curve through a ceiling.

And this is one learning task. Drosophila mushroom body, one acquisition paradigm. It doesn't generalize to "connectomes don't matter" — it says something narrow and checkable.

Everything is open: the paper, the code, every artifact it cites, including the negative result. The repo also documents 12 compiler defects we hit building the simulation — the blocking one wrote 8 bytes into a 4-byte slot — all filed, fixed upstream, verified.

Full writeup and code: github.com/rickenator/VybFly

Paper (downloads directly): vybfly-paper-relay.aniviza.workers.dev/paper.pdf

If you work on connectomics or biological simulation, I'd genuinely like to know whether you've seen this gating-over-topology pattern elsewhere. It feels like it should generalize, and I don't have the evidence to claim it does.

#computationalneuroscience #connectomics #Drosophila #openscience #research