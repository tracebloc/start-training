[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tracebloc/start-training/blob/main/notebooks/traceblocTrainingGuide.ipynb) [![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE) [![Platform](https://img.shields.io/badge/platform-tracebloc-00C9A7.svg)](https://ai.tracebloc.io)

# Start Training 🚀

Launch an ML training experiment on [tracebloc](https://tracebloc.io/) in under 10 minutes. Connect your account, upload a model, link it to a dataset, configure training parameters, and start benchmarking — all from a single notebook.

## Get started

### Option A: Google Colab (recommended)

No local setup. Click the badge above or:

**👉 [Open in Google Colab](https://colab.research.google.com/github/tracebloc/start-training/blob/main/notebooks/traceblocTrainingGuide.ipynb)**

Copy the notebook to your Drive and start running cells.

### Option B: Run locally

```bash
git clone https://github.com/tracebloc/start-training.git
cd start-training

# Pick the extra that matches your ML framework:
pip install "tracebloc[pytorch]>=0.14.0"  # most common
# pip install "tracebloc[sklearn]>=0.14.0" # scikit-learn / boosting
# pip install "tracebloc[all]>=0.14.0"     # everything

jupyter notebook notebooks/traceblocTrainingGuide.ipynb
```

**Which Pythons work:** whatever the SDK's own package metadata declares — see
[`tracebloc` on PyPI](https://pypi.org/project/tracebloc/). This README
deliberately does not repeat the range; a copy here would go stale against the
package, which is exactly the failure this notebook was fixed for
(backend#2862).

If pip answers `No matching distribution found for tracebloc`, that most often
means your interpreter is outside that range rather than the package being
missing — but it can also mean an unreachable index or a custom `--index-url`.
The install cell prints pip's own answer either way: on failure it shows the
range pip actually read alongside the Python you are on. On macOS the default
`python3` is frequently *ahead* of the supported range, so check
`python3 --version` first when running locally.

TensorFlow uploads were removed in SDK 1.0.0, so there is no `[tensorflow]`
extra — the extras are `[pytorch]`, `[sklearn]`, `[catboost]`, `[lightgbm]`,
`[xgboost]`, `[lifelines]`, `[scikit-survival]` and `[all]`.

## What the notebook covers

| Step | What you do |
|:---:|---|
| **1** | Connect to tracebloc with your email + password |
| **2** | Upload a model from the [model zoo](https://github.com/tracebloc/model-zoo) or your own |
| **3** | Link it to a dataset from your use case |
| **4** | Configure training — epochs, batch size, learning rate, augmentation |
| **5** | Start training — model runs inside your secure Kubernetes environment |

Results appear on the use case leaderboard in the [tracebloc web app](https://ai.tracebloc.io/).

## Before you start

- A **tracebloc account** — [sign up free](https://ai.tracebloc.io/signup)
- An **active use case** with a dataset — [how to join one](https://docs.tracebloc.io/join-use-case/)
- A **model file** — grab one from the [model zoo](https://github.com/tracebloc/model-zoo) or [build your own](https://docs.tracebloc.io/join-use-case/model-optimization)

## Links

[Platform](https://ai.tracebloc.io/) · [Docs](https://docs.tracebloc.io/) · [Model zoo](https://github.com/tracebloc/model-zoo) · [PyPI package](https://pypi.org/project/tracebloc/) · [Discord](https://discord.gg/tracebloc)

## License

Apache 2.0 — see [LICENSE](LICENSE).

**Need help?** [support@tracebloc.io](mailto:support@tracebloc.io) or [open an issue](https://github.com/tracebloc/start-training/issues).
