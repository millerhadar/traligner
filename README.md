# TRAligner

A Python package for text alignment with specialized support for Hebrew text processing.

## Installation

```bash
pip install traligner
```

## Features

- Text alignment using Smith-Waterman algorithm
- Support for Hebrew text with specialized matching methods
- Handling of abbreviations, gematria, and other Hebrew-specific text features
- Sequence scoring and merging capabilities
- Word embedding support for semantic similarity

## Quick Start

```python
import traligner as ta

# Align two texts
suspect_tokens = ["שלום", "עולם"]
source_tokens = ["שלום", "לעולם"]

alignment_sequences, df_alignment, suspect_matrix, source_matrix = ta.alignment(
    suspect_tokens,
    source_tokens,
    match_score=3,
    mismatch_score=1,
    methods={
        "ortography": ["י", "ו"],
        "extra_seperators": [""],
        "missing_seperators": [""],
        "abbreviation": ["'", '"'],
    }
)

# Score the alignment
score, sequences = ta.alignmentScore(alignment_sequences)
print(f"Alignment score: {score}")
```

## Advanced Usage

### Using Word Embeddings

```python
# Initialize embedding model
from traligner import EmbeddingRapper
model = EmbeddingRapper(model_path="path/to/fasttext/model.bin")

# Use in alignment
methods = {
    "embeding": {
        "model": model,
        "threshold": 0.7
    }
}

alignment_sequences, df_alignment, suspect_matrix, source_matrix = ta.alignment(
    suspect_tokens,
    source_tokens,
    methods=methods
)
```

### Hebrew Text Analysis

```python
from traligner import HebAnalysis
analyzer = HebAnalysis(mpath="path/to/models")
result = analyzer.base_form("בראשית ברא אלהים")
```

## License

MIT