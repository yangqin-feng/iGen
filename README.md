# iGen

This repository contains the RetiGlobe/DINOv2 model code and Jupyter notebooks for retinal image feature extraction, training, and evaluation. The main workflows are demonstrated in the notebooks at the repository root.

## Requirements

- Linux is recommended. The environment file targets **Python 3.9**, **PyTorch 2.0.0**, **torchvision 0.15.0**, and **CUDA 11.7**.
- An NVIDIA GPU with a compatible CUDA driver is recommended for model training and inference. CPU execution may be very slow and some workflows require CUDA.
- Install Anaconda or Miniconda and Git.
- The DINOv2 environment uses `xformers` and the environment file includes `cuml-cu11`; these are CUDA/Linux-oriented packages. macOS/MPS and Windows are not covered by the supplied environment and may require replacing these dependencies and adjusting the code.

## Installation

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd iGen
```

Replace `<YOUR_GITHUB_REPOSITORY_URL>` with the URL of the GitHub repository after you create it.

### 2. Create the Conda environment

The included `conda.yaml` records the original environment, including Python 3.9, PyTorch 2.0.0, torchvision 0.15.0, and CUDA 11.7.

```bash
conda update -n base -c defaults conda -y
conda env create -f conda.yaml
```

### 3. Activate the environment

```bash
conda activate Retiglobe
```

The environment name is `Retiglobe` as specified in `conda.yaml`.

### 4. Install the remaining Python packages

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

The requirements file pins PyTorch and torchvision to the versions used in the Conda environment. These versions are paired with CUDA 11.7 in the supplied setup; avoid upgrading one independently of the other or of `xformers`.

### 5. Check GPU availability

```bash
nvidia-smi
python -c "import torch; print('PyTorch:', torch.__version__); print('CUDA available:', torch.cuda.is_available())"
```

`CUDA available` should print `True` on a correctly configured NVIDIA system. The CUDA toolkit (`nvcc`) is not always needed to run PyTorch; the NVIDIA driver must support the CUDA runtime installed with PyTorch.

## Running the code

Open the relevant notebook from the repository root using Jupyter, for example:

```bash
conda activate Retiglobe
jupyter lab
```

The notebooks contain the project workflows for preprocessing, training, feature extraction, and evaluation. Before running one, update its data, output, and checkpoint paths to match your local setup. `create_pretrained_model.py` loads `RetiGlobe.pth` from the current directory to construct the pretrained vision model; run it from the repository root:

```bash
python create_pretrained_model.py
```

Training and evaluation require the datasets and checkpoints referenced by the selected notebook. They are not installed by `requirements.txt` and may need to be obtained separately. Do not assume the sample CSV files in the repository contain the image data itself.

## Data and checkpoints

Keep your image datasets and large model checkpoints in local storage, then update the corresponding paths in the notebook or script you use. Check dataset permissions and repository size before uploading data or checkpoint files to GitHub. A `.gitignore` entry for local data and checkpoint files can help prevent accidental uploads.

## Environment files

- `conda.yaml` describes the original Conda environment and CUDA-related packages.
- `requirements.txt` lists Python dependencies for pip installation.

