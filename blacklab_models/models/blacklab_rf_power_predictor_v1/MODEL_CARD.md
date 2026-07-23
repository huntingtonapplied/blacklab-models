---
craft_id: blacklab_rf_power_predictor_v1
version: 0.2.0
project: blacklab
license: Apache-2.0
tags: ['status:trained', 'project:blacklab', 'provenance:engine_truth', 'release_metric:skill_vs_mean']
library_name: blacklab-models
---

# blacklab_rf_power_predictor_v1

**Project:** blacklab · **Version:** 0.2.0 · **License:** Apache-2.0
**Produced by:** [Intel — Universal ML Inference Engine](https://huntingtonai.com)

> Blacklab 2-D RF Power-Map Predictor

> ✅ **Engine-truth data (`engine_truth`).** Targets are direct real simulation-engine output; the headline is the **`ood_r2`** metric.
>
> _Eval note:_ LOOP-CLOSED: Gap-C fixed at the engine (tx-placement arg) → high-variance engine-truth corpus. OOD R² on the disjoint placement-varying band -3.01->+0.9975 (was -6.59 on the low-variance band). Every freq/power bucket beats mean (~0.99). Also fixed a stale-sample-read bug in the engine adapter.

## Model description

`blacklab_rf_power_predictor_v1` is a **surrogate model** ("craft") used by the AHL Intel inference
engine to replace expensive numerical simulation with fast neural inference.
Output kind: **fields** (0 outputs). Blacklab 2-D RF Power-Map Predictor

- **Status:** trained
- **Type:** neural inference surrogate (physics-trained)
- **Parameters:** 34,177
- **Weights format:** `model.safetensors` (float32)
- **Device family:** `—`

## Intended use

Drop-in inference surrogate for blacklab. You provide a physical **device
specification** (geometry, materials, doping, operating point); the package
returns the physical output channels below. The device→model featurization and
de-normalization are handled inside the package. Not intended for regimes
outside its training domain (below).

## Inputs & outputs

**Input — physical device specification** (`input.kind: device_spec`):

Provide a physical device/scene specification; see the project's model docs.

The internal encoding (how the device becomes model inputs) and the normalization are handled **inside the package** — you never build feature vectors by hand.

**Output — physical fields:**

| | |
|---|---|
| **Output channels** | 0 |
| **Parameters** | 34,177 |

## Training domain / compatibility

| Property | Value |
|---|---|
| Solution type | `—` |
| Physics models | — |
| Temperature | — K |
| Bias range (Vds) | — |
| Tags | `status:trained`, `project:blacklab`, `provenance:engine_truth`, `release_metric:skill_vs_mean` |

## Training data

Trained on blacklab simulation output for the `—` solution regime (physics models: see config). Labels derive from the numerical blacklab engine / reference closed-forms; the data-generation pipeline is proprietary.

## Limitations & out-of-scope use

- **Do not** use outside the training domain above (solution type, temperature, bias range) — accuracy degrades with no guarantee.
- This is a **surrogate**, not the ground-truth solver: treat outputs as fast approximations; validate against the numerical engine where correctness is critical.
- Output kind is **fields** — consuming code must match the documented I/O contract exactly.


## Evaluation

| Metric | Value |
|---|---|
| **Held-out accuracy** | 0.9975 |
| Best validation loss | 0.0015134582645259798 |

_**Held-out accuracy** is an independent benchmark (`offline_eval` on a held-out set); the loss rows are the model's own recorded train/val losses. See `config.json → metrics` for the machine-readable copy._

## Caveats & recommendations

- An independent **held-out** benchmark is reported (Held-out accuracy, via `offline_eval`); the loss rows remain the model's own recorded train/val losses.
- Verify integrity before use: `shasum -a 256 -c SHA256SUMS` (or `sha256sum -c SHA256SUMS` on Linux). Weights are `safetensors` — safe to load, no pickle.
- This is a **surrogate**, not the ground-truth solver — validate against the numerical engine where correctness is critical.

## Usage

Install the inference package and run it on a physical device spec — it fetches the
weights, builds the model, and returns physical fields (no PyTorch required):

```bash
pip install blacklab-models
```

```python
from blacklab_models import load

model = load("blacklab_rf_power_predictor_v1")           # pulls + verifies weights, builds the compiled pipeline
fields = model.predict(device_spec)  # physical device in -> physical fields out
```

`device_spec` is the physical device specification documented under **Inputs & outputs**
above. Featurization and de-normalization happen inside the package.

## Provenance

- **Author:** sim-train release (NONBOLTZMANN_RELEASE_TRAINING.md)
- **Trained:** 2026-07-18T17:34:54.193215+00:00
- **Source checksum (runtime .pt):** `c398daa4a5c55bb533eb77bb47a706b1754c026ade8fce2fa09acad3876bd263`

## Citation

```bibtex
@software{blacklab_rf_power_predictor_v1_0_2_0,
  title  = {blacklab_rf_power_predictor_v1},
  author = {AHL / Intel},
  year   = {2026},
  note   = {Version 0.2.0},
  url    = {https://downloads.blacklab.world/models/blacklab_rf_power_predictor_v1/0.2.0/}
}
```

## License

Licensed under the **Apache-2.0** (Apache-2.0) — free to use for
inference; redistribution and reverse engineering of the compiled inference core
are not permitted. See `LICENSE`.
