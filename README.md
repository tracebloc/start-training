[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1N00idtpoaq1lk9OJE6g4bMqd8o-Qex2C?usp=sharing) [![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE) [![Platform](https://img.shields.io/badge/platform-tracebloc-00C9A7.svg)](https://ai.tracebloc.io)

# Start Training 🚀

Launch an ML training experiment on [tracebloc](https://tracebloc.io/) in under 10 minutes. Connect your account, upload a model, link it to a dataset, configure training parameters, and start benchmarking — all from a single notebook.

## Get started

### Option A: Google Colab (recommended)

No local setup. Click the badge above or:

**👉 [Open in Google Colab](https://colab.research.google.com/drive/1N00idtpoaq1lk9OJE6g4bMqd8o-Qex2C?usp=sharing)**

Copy the notebook to your Drive and start running cells.

### Option B: Run locally

```bash
git clone https://github.com/tracebloc/start-training.git
cd start-training

# Pick the extra that matches your ML framework:
pip install "tracebloc_package[pytorch]>=0.6.33"      # most common
# pip install "tracebloc_package[tensorflow]>=0.6.33" # TensorFlow
# pip install "tracebloc_package[all]>=0.6.33"        # everything

jupyter notebook notebooks/traceblocTrainingGuide.ipynb
```

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

[Platform](https://ai.tracebloc.io/) · [Docs](https://docs.tracebloc.io/) · [Model zoo](https://github.com/tracebloc/model-zoo) · [PyPI package](https://pypi.org/project/tracebloc-package/) · [Discord](https://discord.gg/tracebloc)

## License

Apache 2.0 — see [LICENSE](LICENSE).

**Need help?** [support@tracebloc.io](mailto:support@tracebloc.io) or [open an issue](https://github.com/tracebloc/start-training/issues).
