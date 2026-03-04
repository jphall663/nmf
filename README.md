NMF Text Pipeline
================================

Overview
- Preprocesses raw text into a term-by-document (TBD) matrix.
- Decomposes the TBD matrix into interpretable features via alternating-least-squares NMF.
- Postprocesses features by naming topics and clustering documents.

Repository Structure
- `Preprocess.py`: Text cleaning, lemmatization, stoplisting, and TBD matrix creation.
- `NMF.py`: ALS-based NMF implementations for dense/sparse matrices.
- `Postprocess.py`: Feature sorting/naming and document clustering.
- `BatchDriver.py`: End-to-end batch pipeline.
- `scripts/`: Additional utilities (graph export).
- `data/`: Example input datasets (e.g., `mlhra_corpus.txt`, `sample_data.txt`).
- `stoplist/`: Stoplist files consumed by `Preprocess.py`.
- `replacements/`: Lemmatization/replacement dictionaries (`rai_replacements.txt`).

Requirements
- Python 3.9+
- Install packages from `requirements.txt`.
- Optional: Gephi (to visualize graphs exported by `scripts/make_gdf.py`).

Setup
1) Create/activate a Python 3 environment.
2) Install dependencies: `python3 -m pip install -r requirements.txt`.
3) Download NLTK WordNet data (for lemmatization):
   - `python3 -c "import nltk; nltk.download('wordnet')"`

Data
1) Place your corpus files in `data/` (examples: `data/mlhra_corpus.txt`, `data/rai_training_corpus.txt`).
2) A small test dataset is available at `data/sample_data.txt`.
3) Outputs and intermediates are written to the working directory configured in drivers (defaults to `results/`).

Run: Batch Pipeline (primary)
1) From the repo root, ensure imports resolve by setting `PYTHONPATH=.`
2) Adjust parameters in `BatchDriver.py` if needed (e.g., `nthread`, `n_features`, `threshold`). To use a custom replacements file, set `custom_replacements` to a path under `replacements/`.
3) Run the pipeline:
   - `PYTHONPATH=. python3 BatchDriver.py`

Scripts
- `scripts/make_gdf.py`: Generate a GDF graph from an H matrix produced by a pipeline run (adjust hard-coded paths/filenames as needed).

Run: Tests
1) From the repo root:
   - `PYTHONPATH=. python3 tests/TestPreprocess.py`
   - `PYTHONPATH=. python3 tests/TestNMF.py`
   - `PYTHONPATH=. python3 tests/TestPostprocess.py`

Export Graph for Gephi (optional)
1) After running NMF, confirm the H-matrix path in `scripts/make_graph_script2.py` (defaults to a file in `results/`).
2) Generate a GDF file:
   - `PYTHONPATH=. python3 scripts/make_gdf.py`
3) Open the resulting `graph.gdf` in Gephi and explore:
   - Layout: Force Atlas → Run → Stop
   - Community detection: Modularity → Run
   - Appearance: Nodes → Partition → Color → Modularity class
   - Labels, Preview, Export

Conventions
- Keep large/private datasets out of version control; store them under `data/` locally.
- Default working directory for generated artifacts is `results/`; adjust in drivers if needed.
