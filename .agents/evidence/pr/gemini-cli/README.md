# Gemini CLI PR Evidence

Generated from real Gemini CLI OAuth / Code Assist runs on 2026-05-13.

## Commands

```bash
PROMPT='Real claude-tap validation for Gemini. Use shell to run pwd and test whether pyproject.toml exists. Then answer with exactly: VALIDATION_CLIENT=gemini, PWD=<pwd>, PYPROJECT_EXISTS=<true|false>.'
timeout 240 uv run python -m claude_tap --tap-client gemini --tap-output-dir .traces/real-validation --tap-no-open --tap-no-update-check -- --skip-trust -p "$PROMPT" --yolo --output-format text

PROMPT='Second-turn claude-tap validation for Gemini. Continue the previous session. Use shell to run: printf "VALIDATION_CLIENT=gemini SECOND_TURN=true\n"; pwd. Then answer with exactly those two facts.'
timeout 240 uv run python -m claude_tap --tap-client gemini --tap-output-dir .traces/real-validation --tap-no-open --tap-no-update-check -- --skip-trust --resume latest -p "$PROMPT" --yolo --output-format text
```

## Results

- First turn: `.traces/real-validation/2026-05-13/trace_121407.jsonl`, 15 POST records, final output `VALIDATION_CLIENT=gemini, PWD=/home/liaohch3/src/github.com/liaohch3/claude-tap-3, PYPROJECT_EXISTS=true`.
- Resume turn: `.traces/real-validation/2026-05-13/trace_121438.jsonl`, 13 POST records, final output `VALIDATION_CLIENT=gemini SECOND_TURN=true` plus the repo path.
- Hosts captured: `cloudcode-pa.googleapis.com`, `oauth2.googleapis.com`, and `play.googleapis.com`.
- Generation endpoint captured: `/v1internal:streamGenerateContent?alt=sse`.

## Screenshots

- `first-01-overview.png`
- `first-02-expanded-sections.png`
- `first-03-detail-mid-scroll.png`
- `first-04-later-turn-scrolled.png`
- `resume-01-overview.png`
- `resume-02-expanded-sections.png`
- `resume-03-detail-mid-scroll.png`
- `resume-04-later-turn-scrolled.png`

## Validation

```bash
uv run ruff check .
uv run ruff format --check .
uv run pytest tests/ -x --timeout=60
uv run python scripts/check_screenshots.py .agents/evidence/pr/gemini-cli
uv run python scripts/verify_screenshots.py .traces/real-validation/2026-05-13/trace_121407.html .traces/real-validation/2026-05-13/trace_121438.html
```
