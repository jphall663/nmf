## Tests

- Location: All unit tests live in `tests/`.
- Purpose: Exercise the preprocessing, NMF, and postprocessing stages on small/simulated data.

### Test Files
- `TestPreprocess.py`: Runs the full preprocessing chain against `data/sample_data.txt`.
- `TestNMF.py`: Exercises the NMF implementations on simulated sparse data.
- `TestPostprocess.py`: Runs preprocessing + NMF, then tests postprocessing on the generated matrices.

### How to Run
- From the repo root with Python 3:
  - `PYTHONPATH=. python3 tests/TestPreprocess.py`
  - `PYTHONPATH=. python3 tests/TestNMF.py`
  - `PYTHONPATH=. python3 tests/TestPostprocess.py`

Notes
- Tests assume input data under `data/` and will write intermediates to `results/` by default.
