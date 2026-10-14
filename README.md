# GNN for Biological Interaction Networks

Capstone project: a Graph Neural Network framework built on the human protein–protein interaction
network for **protein function prediction** (node classification) and **disease association prediction**.
Models: GCN, GAT, GraphSAGE · Explanations: GNNExplainer · App: Streamlit (to be moved to React later).

Scope: human proteins only (NCBI taxon 9606).

## Environment

| Component | Version |
|---|---|
| Python | 3.11 (project-local `.venv`) |
| PyTorch | 2.14.1, CUDA 13.0 build |
| PyTorch Geometric | 2.8.1 + pyg-lib 0.9.0 |
| Protein language models | Hugging Face `transformers` (ESM-2, ProtBERT) |

The full list of packages is in `requirements.txt`.

### Setup (Windows, PowerShell)

```powershell
py -3.11 -m venv .venv
.venv\Scripts\python -m pip install --upgrade pip
.venv\Scripts\python -m pip install -r requirements.txt
```

`requirements.txt` already points pip at the PyTorch CUDA 13.0 index and the PyG wheel index.
GPU support needs an NVIDIA driver that supports CUDA 13.0 or newer (check with `nvidia-smi`).

### VS Code + Jupyter

1. Install the **Python** and **Jupyter** extensions (`ms-python.python`, `ms-toolsai.jupyter`).
2. Open this folder in VS Code. `.vscode/settings.json` points VS Code at `.venv`.
3. Open a notebook and click **Select Kernel** (top right) → **Python Environments** → `.venv`.
4. Run `notebooks/00_environment_check.ipynb`. Every cell should finish without errors.

Notebooks run with the project root as their working directory, so paths like `data/raw/...`
work from every notebook.

`ipywidgets` is deliberately **not** installed. With VS Code 1.141 and Jupyter extension 2025.9.1,
the first widget of each session fails to load and VS Code shows a "download supporting files from
a 3rd party website" dialog. Without ipywidgets, `tqdm` progress bars are plain text, and the
notebooks hide tqdm's "IProgress not found" hint. Don't install ipywidgets back.

## Folder structure

```
data/raw/         downloaded datasets (UniProt, STRING, GO, disease data), not committed
data/processed/   cleaned tables, protein embeddings, graph objects, not committed
notebooks/        pipeline notebooks, run in order (00_, 01_, ...)
src/              reusable Python code (models, helpers) shared by the notebooks and the app
models/           trained model checkpoints, not committed
results/          figures and metrics
```
