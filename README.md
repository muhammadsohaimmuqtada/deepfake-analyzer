# AI Text Humanizer

A local text-rewriting toolkit for reducing repetitive model-like phrasing and giving generated drafts more varied sentence structure, contractions, vocabulary, and rhythm.

The project runs locally and provides a GUI, CLI, Python API, and optional FastAPI service.

> This tool is best treated as a writing and editing experiment. It does not guarantee that text will be classified as human-written by AI-detection systems, and detector scores should not be treated as reliable measures of authorship.

## Features

- multi-stage rewriting pipeline
- common AI-style phrase cleanup
- contraction insertion
- clause reordering
- sentence splitting and merging
- configurable lexical variation
- deterministic runs with an optional random seed
- Tkinter desktop GUI
- CLI and Python API
- optional FastAPI service
- local execution with no required external model API

## Pipeline

The current rewriting pipeline applies a combination of:

1. marker and phrase cleanup
2. sentence tokenization
3. contraction insertion
4. clause reordering
5. sentence splitting
6. sentence-length variation
7. limited discourse-marker insertion
8. configurable synonym substitution

These transformations are heuristic. They can improve variety in some drafts but may also alter tone or introduce awkward wording, so final human review is expected.

## Installation

```bash
git clone https://github.com/muhammadsohaimmuqtada/AI-text-humanizer.git
cd AI-text-humanizer

python3 -m venv .venv
source .venv/bin/activate
pip install -e '.[api]'
```

Download the optional NLTK resources used by the richer NLP path:

```bash
python -m nltk.downloader wordnet punkt_tab averaged_perceptron_tagger_eng
```

## GUI

```bash
aip-gui
```

or:

```bash
python -m aip.gui
```

The GUI provides preset rewrite strengths plus custom controls for transformation rates.

## CLI

```bash
aip humanize --text "Your draft goes here." --pretty
```

Runtime checks:

```bash
aip doctor --pretty
aip preflight --pretty
```

Start the optional API service:

```bash
aip serve --port 8000
```

## Python API

```python
from aip.humanizer import humanize

result = humanize(
    text="Your draft goes here.",
    synonym_rate=0.20,
    merge_rate=0.20,
    seed=42,
)

print(result.humanized_text)
```

## API

`POST /humanize` accepts text and transformation settings and returns the rewritten text with basic processing metadata.

Operational endpoints include:

- `GET /healthz`
- `GET /readyz`
- `GET /doctor`
- `GET /policies`
- `GET /metrics`

## Privacy

- rewriting is performed locally
- no model API is required for the core pipeline
- no built-in telemetry is required for local use
- clipboard actions are user initiated

## Testing

```bash
pip install -e '.[test]'
python -m pytest tests/ -v
```

## Project documentation

- [SECURITY.md](SECURITY.md)
- [DEPLOYMENT.md](DEPLOYMENT.md)
- [CONTRIBUTING.md](CONTRIBUTING.md)
- [CHANGELOG.md](CHANGELOG.md)

## License

MIT License.