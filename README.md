# blacklab-models

Runnable neural-surrogate inference package for **blacklab** — compiled and torch-free (ONNX + `onnxruntime`, CPU). Physical spec in, physical results out.

```python
from blacklab_models import load, list_models
model = load(list_models()[0])
```

## Install

Preview packages are proprietary and are **not on PyPI**, so `pip install blacklab-models` will not resolve. Install the wheel directly from the GitHub release:

```
pip install https://github.com/huntingtonapplied/blacklab-models/releases/download/v0.2.1/blacklab_models-0.2.1-py3-none-any.whl
```

Dependencies: `numpy`, `onnxruntime` (CPU) — no torch. A hosted package index (so `pip install blacklab-models` resolves directly) is planned.

## License

Closed-source, compiled distribution. Licensed under the **Blacklab Model EULA** (see `LICENSE`). Reverse engineering, weight/feature extraction, and redistribution are prohibited. © 2025-2026 Huntington Applied.
