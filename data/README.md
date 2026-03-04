## Data Folder

- Purpose: Centralize input datasets used by drivers and tests.

- Files:
  - `mlhra_corpus.txt`: Main corpus consumed by drivers (e.g., `BatchDriver.py`).
  - `sample_data.txt`: Small sample used by unit tests.

- Conventions:
  - Reference data files with paths like `data/<filename>` in drivers and tests.
- Outputs, intermediates, and large generated artifacts should go to a separate working directory (e.g., `results/` via the `working_dir` setting), not into `data/`.
  - Stoplists currently live under `stoplist/` at repo root; keep `stop_dir = 'stoplist'` unless you relocate them to `data/stoplist/` and update code accordingly.

- Notes:
  - Formats are plain text; each line represents one logical record/document as expected by `Preprocess.py`.
  - Large or private datasets should not be committed. Consider adding them to `.gitignore`.
