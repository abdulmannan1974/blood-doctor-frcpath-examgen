# Exam Material Generator

This toolkit ingests local sources and generates FRCPath haematology exam materials using the Blood Doctor framework. It outputs both DOCX and PDF.

## Quick Start

1. Drop source files into `examgen/sources/`.
2. Edit `examgen/project.yaml` (counts, scope, outputs, model).
3. Run:

```bash
python3 examgen/generate.py --config examgen/project.yaml
```

Outputs are written to `examgen/out/`.

## Inputs Supported

- PDF (.pdf)
- Word (.docx)
- PowerPoint (.pptx)
- Excel or CSV (.xlsx, .xls, .csv)
- Images (.png, .jpg, .jpeg) with OCR if `pytesseract` is installed
- Text or Markdown (.txt, .md)

## Outputs

- DOCX (via python-docx)
- PDF (via reportlab)
- A raw Markdown file for traceability

## AI Assisted Mode

Set your API key before running:

```bash
export OPENAI_API_KEY="YOUR_KEY"
```

You can switch to template-only mode by setting:

```yaml
generation:
  mode: "template"
```

## Notes on Sources

This build is **local files only**. For Google Docs, Slides, or YouTube:

- Export Google Docs/Slides as PDF or DOCX and drop them into `sources/`.
- For YouTube, export a transcript to a text file and drop it into `sources/`.
- For websites, save as PDF and drop into `sources/`.

## Dependencies

Install required Python packages:

```bash
python3 -m pip install -r examgen/requirements.txt
```

If you want OCR from images, install Tesseract:

```bash
brew install tesseract
```

## File Map

- `examgen/generate.py` main generator
- `examgen/project.yaml` configuration
- `examgen/templates/framework_excerpt.md` prompt guidance
- `examgen/sources/` input files
- `examgen/out/` outputs

## Customization

- Increase counts in `project.yaml` for larger packs
- Add more sources to cover more domains
- Adjust `generation.source_policy` to `hybrid` to allow general knowledge when sources are thin
- Use `domains` and `section_domain_map` in `project.yaml` to improve section-level retrieval
- Use `generation.require_keyword_match` to force SOURCE GAP when sources are not relevant
