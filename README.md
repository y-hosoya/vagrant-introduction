# Template-mkdocs

## Usage

### Local

activate python3 env

```bash
git clone git@github.com:ymmmtym/template-mkdocs.git
cd template-mkdocs
python3 -m venv --clear .venv
. .venv/bin/activate
pip install -r requirements.txt
```

build

```bash
mkdocs build
```

run

```bash
mkdocs serve -a 0.0.0.0:8000
```

### Github Pages

Push to main branch.
