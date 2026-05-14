# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo does

Jupyter notebook quick-start guide for running ML training experiments on the tracebloc platform. Walks users through connecting their account, uploading a model, linking a dataset, configuring training parameters, and starting an experiment.

## Notebook locations

- `notebooks/traceblocTrainingGuide.ipynb` -- main training guide (also available on [Google Colab](https://colab.research.google.com/drive/1N00idtpoaq1lk9OJE6g4bMqd8o-Qex2C?usp=sharing))
- `notebooks/GenerateCheckWeights.ipynb` -- utility for generating/checking model weights

## How users run it

### Google Colab (recommended)
Open the Colab link, copy to Drive, and run cells.

### Locally
```bash
pip install "tracebloc[pytorch]>=0.8.1"
jupyter notebook notebooks/traceblocTrainingGuide.ipynb
```

## Prerequisites

- A tracebloc account
- An active use case with a dataset
- A model file (from the [model-zoo](https://github.com/tracebloc/model-zoo) repo or custom)

## Key dependency

[`tracebloc`](https://pypi.org/project/tracebloc/) (PyPI, 0.8.x+) -- the Python SDK used in the notebook to authenticate, upload models, and start training.

> Was published as `tracebloc_package` before 0.8.0. The old install command (`pip install tracebloc_package`) still resolves via a metadata-only redirect on PyPI, but new notebooks should use the canonical `tracebloc` name.
