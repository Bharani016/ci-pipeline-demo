# CI Pipeline Demo

![CI](https://github.com/Bharani016/ci-pipeline-demo/actions/workflows/test.yml/badge.svg)

A small Python calculator used to demonstrate an automated multi-version CI pipeline with GitHub Actions.

Every push and pull request to `main` automatically runs linting, a formatting check and the unit tests on Python 3.10, 3.11 and 3.12.

---

## Project Structure

```text
.
├── .github/workflows/test.yml   # CI workflow
├── app/
│   ├── __init__.py
│   └── calc.py                  # calculator functions
├── tests/
│   ├── __init__.py
│   └── test_calc.py             # pytest unit tests
├── requirements.txt             # pytest, flake8, black
├── LICENSE
└── README.md
```

---

## Run Locally

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

python -m flake8 app tests
python -m black --check app tests
python -m pytest -v
```

---

## How the Pipeline Works

Workflow file: `.github/workflows/test.yml`

| Feature | Detail |
|---------|--------|
| Triggers | Push and pull request to `main` |
| Matrix | Python 3.10, 3.11, 3.12 |
| Lint | `flake8 app tests` |
| Format check | `black --check app tests` |
| Tests | `pytest -v` |
| Caching | `cache: pip` in `actions/setup-python` |
| Failure behaviour | Any failing step exits non-zero and marks the run red |

If any step fails, the job fails. With branch protection enabled, a pull request with a failing check cannot be merged.

---

## Branch Protection

The `main` branch requires a pull request and the three status checks (`test (3.10)`, `test (3.11)`, `test (3.12)`) to pass before merging.

---

## Failure Scenario

A pull request that deliberately contains a failing test shows the pipeline going red and the merge button being blocked. After the test is fixed, the checks turn green and the pull request can be merged.

---

## Execution Evidence

### Passing run

_Screenshot to be added._

### Failing pull request

_Screenshot to be added._

### Blocked merge

_Screenshot to be added._

### Cache restored

_Screenshot to be added._

---

## Execution Logs

_Log excerpts to be added._

---

## Commit Convention

Commits follow Conventional Commits: `feat`, `fix`, `test`, `chore`, `ci`, `docs`.

---

## License

MIT License. See `LICENSE`.
