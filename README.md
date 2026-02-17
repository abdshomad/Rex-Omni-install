# Rex-Omni Installation

Installation and development environment for [Rex-Omni](https://github.com/IDEA-Research/Rex-Omni).

## Prerequisites

- Python 3.11+
- [uv](https://docs.astral.sh/uv/) package manager
- CUDA-capable GPU (for model inference)
- Linux: `python3.12-dev` (for building extensions)

  ```bash
  sudo apt-get update && sudo apt-get install -y python3.12-dev
  ```

## Installation

### 1. Clone and initialize submodule

```bash
git clone <this-repo-url>
cd Rex-Omni-install
git submodule update --init --recursive
```

The Rex-Omni submodule: https://github.com/IDEA-Research/Rex-Omni

### 2. Create virtual environment and sync dependencies

```bash
uv venv
source .venv/bin/activate
uv sync
```

### 3. Install PyTorch (required by flash-attn)

```bash
uv pip install torch
uv sync --no-build-isolation
```

### 4. Install Rex-Omni in editable mode

```bash
cd Rex-Omni
uv pip install -v -e .
cd ..
```

## Run Detection Example

```bash
CUDA_VISIBLE_DEVICES=1 uv run python Rex-Omni/tutorials/detection_example/detection_example.py
```

**Expected output:** `Visualization saved to: Rex-Omni/tutorials/detection_example/test_images/cafe_visualize.jpg`

On first run, models are downloaded (multi-GB); progress will look like:

```
Initializing transformers backend...
config.json: 1.49kB [00:00, 9.71MB/s]
model.safetensors.index.json: 65.5kB [00:00, 268MB/s]
Fetching 2 files:   0%|                                 | 0/2 [00:00<?, ?it/s]
model-00001-of-00002.safetensors:   6%|▏  | 307M/5.00G [01:47<12:54, 6.05MB/s]
model-00002-of-00002.safetensors:  29%|▉  | 916M/3.14G [01:47<01:52, 19.7MB/s]
```
