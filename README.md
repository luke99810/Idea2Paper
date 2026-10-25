# Idea2Paper

A local agent skill and reproducible research toolkit: research question → evidence → model → computation → figures → manuscript → review.

This repository contains reusable skill instructions, Python utilities, templates, offline tests, and a synthetic logistics teaching example. It does not automate scientific judgment or certify publication readiness.

## Quick start

Python 3.10+ is required. The evidence workflow uses the standard library. Manuscript rendering additionally requires `python-docx` and `Pillow`:

    uv run --with python-docx --with Pillow python -m unittest discover -s tests -v
    python scripts/paper.py --help
    python scripts/paper.py demo examples/my-new-demo
    python scripts/paper.py validate examples/my-new-demo

Load `SKILL.md` in your agent before applying the research workflow. The package is portable and does not automatically modify global skills or agent settings. The demo command refuses to overwrite an existing directory.

## Manuscripts

Maintain the manuscript in `draft/manuscript.md`, then render:

    uv run --with python-docx --with Pillow python scripts/render.py latex examples/logistics-demo
    uv run --with python-docx --with Pillow python scripts/render.py docx examples/logistics-demo

LaTeX output uses `templates/latex/manuscript.tex`. XeLaTeX is optional; if unavailable, the command reports that PDF compilation was not performed. Word-to-PDF export requires an actual Word/WPS/LibreOffice installation and is not included in the portable CLI. Do not treat an old PDF as a new successful export.

The checked-in `examples/logistics-demo/draft/manuscript.pdf` is a preview generated with Microsoft Word 16.0 on Windows. The corresponding LaTeX source was generated but not compiled locally. Review and regenerate the preview after changing source files.

## Layout rules

- Independent centered manuscript title; section headings do not inherit body indentation.
- Ordinary Chinese body paragraphs use approximately two-character first-line indentation and 1.5 line spacing; abstract, captions and table cells do not.
- All figure text is English in actual Times New Roman. Font substitution is forbidden when that font is requested; install a legally licensed copy or provide it in a supported font location.
- Raster figures must have at least 300 effective dpi at their final embedded width. Legends, labels and other elements must not obscure each other or be clipped.
- Three-line editable tables; numeric values and percent signs must not be split across lines. Column widths require content-aware review, not just a fixed column count.
- Citation style is project-configurable. The teaching example explicitly selects numeric `[1]` citations through `render-config.json`, overriding its historical journal adaptation record. Numeric labels are not claimed to be Transportation Science's official style.
- Mechanical checks and PDF visual review are separate requirements. Passing tests does not certify scientific validity or journal compliance.

Detailed rules: `references/rendering.md`, `references/figures-writing.md`, and `references/journal-adaptation.md`.

## Published teaching example

`examples/logistics-demo` includes authored code, synthetic demand, computed JSON/CSV, SVG figures, a Markdown manuscript, LaTeX source and PDF preview. It uses no production/company data. References were checked at metadata level only; no full-text reading is claimed. The underlying simulation is a teaching fixture, not a validated model for operational decisions.

The curated example intentionally excludes local execution logs, run records, caches, old versions, machine-specific environment information and sealed manifests. It is not a complete archived evidence package and must not be passed off as a `paper.py validate`-approved research project. To obtain a complete runnable evidence-chain example, execute the fresh `paper.py demo` command above.

## Repository contents

- `SKILL.md`: stage gates, approval points and evidence discipline.
- `scripts/`: project creation, execution records, provenance checks, DOI lookup and manuscript conversion.
- `templates/`: initial project evidence files and LaTeX skeleton.
- `references/`: procedural requirements and scientific limitations.
- `tests/`: offline regression tests using synthetic fixtures.

No automatic submission, publishing, paid APIs, restricted data downloads or production operations are performed by the research CLI. Commands executed by the runner are not sandboxed; inspect code and authorize inputs before running it.

## Verification and limitations

Offline suite verified on Windows with Python 3.11, python-docx and Pillow. Linux/macOS have not been exercised end-to-end; font-dependent tests require Times New Roman. SVG conversion supports a limited explicit subset and rejects unsupported required elements. DOI metadata verification does not establish that a source supports a scientific claim.

License: see `LICENSE`. Third-party journal articles and font files are not distributed.
