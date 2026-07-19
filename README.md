# blacklab-models

Runnable neural-surrogate inference for the **Blacklab** multi-sensor perception platform.
Model inputs in, physical outputs out, torch-free (ONNX + `onnxruntime`, CPU).

```python
from blacklab_models import load

model = load("blacklab_rf_power_predictor_v1")
out = model.predict(inputs={"scene_grid": scene})   # scene: [B, 7, H, W, 1]
rf_power_dbm = out["rf_power"]                        # [B, 1, H, W, 1] in physical dBm
```

Runs at any grid resolution. `model.input_names` / `model.output_names` and each craft's
`MODEL_CARD.md` document the exact I/O.

## Install

```
pip install blacklab-models      # numpy + onnxruntime only, no torch
```

## Scope

- **Preview build**: ships `blacklab_rf_power_predictor_v1`; more crafts follow.
- **Fast surrogates, not the ground-truth solver.**

## License

Closed-source, compiled distribution under the **AHL Model EULA** (see `LICENSE`).
© 2025–2026 Huntington Applied.
