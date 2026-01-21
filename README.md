# code-diff-ast

A CLI tool that maps git diffs to AST (Abstract Syntax Tree) nodes for LLM consumption. Instead of raw diff output, get structured JSON with semantic information about what functions, classes, and methods changed.

## Installation

```bash
pip install code-diff-ast
```

## Usage

### Diff staged changes (default)

```bash
code-diff
```

### Diff unstaged working directory changes

```bash
code-diff --working
```

### Compare branches or commits

```bash
code-diff --from main --to HEAD
code-diff --from abc123 --to def456
```

### Output options

```bash
# Save to file (default: diff.json)
code-diff -o changes.json

# Print to stdout
code-diff --stdout
```

## Output Format

The tool outputs JSON with changes mapped to AST nodes:

```json
{
  "diff_mode": "commits",
  "base_ref": "main",
  "target_ref": "HEAD",
  "files": [
    {
      "path": "src/example.py",
      "status": "modified",
      "language": "python",
      "changes": [
        {
          "type": "function",
          "name": "calculate_total",
          "line_start": 42,
          "line_end": 58,
          "change_type": "modified",
          "diff_lines": [45, 47, 52],
          "signature": "def calculate_total(items):",
          "content": "..."
        }
      ]
    }
  ]
}
```

## Supported Languages

- Python
- JavaScript
- TypeScript
- Go
- Rust

## Contributing

Contributions are welcome!

### Setup

1. Fork and clone the repository:
   ```bash
   git clone https://github.com/YOUR_USERNAME/code-diff.git
   cd code-diff
   ```

2. Install in development mode:
   ```bash
   pip install -e .
   ```

3. Create a branch for your changes:
   ```bash
   git checkout -b my-feature
   ```

### Making Changes

- Source code is in `src/code_diff/`
- `cli.py` - Command-line interface
- `diff_parser.py` - Git diff parsing
- `ast_mapper.py` - Maps changes to AST nodes
- `languages.py` - Language detection and Tree-sitter setup
- `output.py` - Output formatting

### Submitting a PR

1. Commit your changes
2. Push to your fork
3. Open a pull request against `main`

### Adding Language Support

To add support for a new language:

1. Add the Tree-sitter grammar to `pyproject.toml` dependencies
2. Update `languages.py` with file extensions and Tree-sitter setup
3. Add node type mappings for the language's AST

## License

MIT
