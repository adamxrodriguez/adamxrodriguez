# Adam Rodriguez — Senior Software Engineer

I ship production software. React/TypeScript on the front. Node/Next.js and cloud on the back.  
I care about clean systems, fast feedback loops, and work that actually moves the needle.

- **10+ yrs** building enterprise features (healthcare, data, dashboards)
- **React/Next.js, Node, TypeScript, Python**; CI/CD with **GitHub Actions/Jenkins**
- Comfort in the trenches: debugging flaky pipelines, profiling, cost/latency chops

> Some days you don’t feel it.  show up anyway.

---

## Selected Work

- **Metamorphosis (Kafka Observability)** — monitoring  
  Dashboards & tooling that reduce triage time and make message flow visible at a glance.  
  Org repo → https://github.com/oslabs-beta/Metamorphosis

- **Miracle Health (Next.js/TypeScript)** — full-stack features, auth, typed APIs, CI  
  Patterns I like: request validation with Zod, React Query, error boundaries, health checks.  
  Repo → https://github.com/adamxrodriguez/miracle-health

- **Yatch Hub (NextJS/React)** — Yatch dashboard workflow tool  
  Focus on accessibility, keyboard shortcuts, undo/redo, local persistence.  
  Repo → https://github.com/adamxrodriguez/nextjs-dashboard

- **Sofle RGB (keyboard firmware & tooling)** — customization, reproducible builds  
  Notes on low-level configs, ergonomics, and build repeatability.  
  Repo → https://github.com/adamxrodriguez/sofle-rgb-keyboard

---

## How I work

- **Ship small, ship daily.** CI and tests make change cheap and safe.  
- **If it isn’t observable, it isn’t done.** Logs, metrics, traces, healthz.  
- **Pragmatic by default.** Simple > clever. Measure, then optimize.

> I’ve failed more times than I’d admit, but every time I did, I learned something worth keeping.

---

## Toolbox

**Front-end:** React, Next.js, TypeScript, Redux, SWR/React Query, Playwright, Vitest  
**Back-end:** Node, Express/Next API Routes, Python, Kafka, Postgres/Redis  
**DevOps:** GitHub Actions, Jenkins, Docker, OpenAPI  
**Patterns:** rate limiting, idempotency, retries, circuit breakers, feature flags

---

## Case Studies (short reads)

- **Making deployments boring:** wired CI (lint/test/build), added coverage gates, shaved MTTR.  
- **Typed boundaries:** Zod-validated API layer + React Query for cache-aware UX.  
- **Fast feedback:** Playwright smoke tests on PRs; bugs caught before prod.

---

## Contact

- **LinkedIn:** https://www.linkedin.com/in/adamrodriguez  
- **Email:** adamxrodriguez@gmail.com
- **Location:** Florida (EST)

> Don’t wait to feel ready — start.


Great use case — and the “looks horrible” problem is very common. The root issue is usually that converters try to preserve inline CSS instead of mapping to Word’s named styles. Here’s the smartest architecture:
The Recommended Stack
Pandoc + a reference.docx template is far and away the best approach for this:

pandoc input.html -o output.docx --reference-doc=template.docx


Pandoc maps HTML semantic elements (h1, h2, table, ul, code) directly to Word named styles from your template — so your output inherits your org’s fonts, spacing, colors, etc. automatically.

The Two-Stage Python Pipeline
For production quality, wrap pandoc in a Python pre/post-processing pipeline:

HTML (from Windsurf/EXE)
        ↓
  [Stage 1: Clean HTML]
  BeautifulSoup → normalize structure,
  strip inline styles, fix tables
        ↓
  [Stage 2: Convert]
  pandoc → DOCX via reference template
        ↓
  [Stage 3: Post-process (optional)]
  python-docx → inject cover page, TOC,
  fix code blocks, add headers/footers
        ↓
   Final .docx


Stage 1 — Clean the HTML first (this is the real unlock)

from bs4 import BeautifulSoup

def clean_html_for_docx(raw_html: str) -> str:
    soup = BeautifulSoup(raw_html, "html.parser")

    # Strip inline styles — pandoc will use your template styles instead
    for tag in soup.find_all(style=True):
        del tag["style"]

    # Normalize code blocks so pandoc renders them as Word code style
    for pre in soup.find_all("pre"):
        pre["class"] = "code"

    # Fix tables — ensure they have <thead> so pandoc creates header rows
    for table in soup.find_all("table"):
        if not table.find("thead"):
            first_row = table.find("tr")
            if first_row:
                thead = soup.new_tag("thead")
                first_row.wrap(thead)

    return str(soup)


Stage 2 — Convert with pandoc

import subprocess, tempfile, os

def html_to_docx(html: str, template_path: str, output_path: str):
    with tempfile.NamedTemporaryFile(suffix=".html", delete=False, mode="w") as f:
        f.write(html)
        tmp = f.name

    subprocess.run([
        "pandoc", tmp,
        "-o", output_path,
        "--reference-doc", template_path,
        "--toc",                    # auto table of contents
        "--toc-depth=3",
        "--highlight-style=tango",  # code block syntax highlighting
    ], check=True)

    os.unlink(tmp)


Stage 3 — Post-process with python-docx (optional)

from docx import Document

def post_process(docx_path: str):
    doc = Document(docx_path)

    # Example: enforce consistent code block font
    for para in doc.paragraphs:
        if para.style.name == "Source Code":
            for run in para.runs:
                run.font.name = "Courier New"
                run.font.size = Pt(9)

    doc.save(docx_path)


Building the reference.docx Template
This is the highest-leverage thing you can do. Steps:
	1.	Run pandoc --print-default-data-file reference.docx > base_template.docx to get a starter
	2.	Open in Word, go to Styles pane
	3.	Customize: Heading 1–3, Body Text, Source Code, Table, Compact (list items)
	4.	Add your Florida Blue / ECMS logo, header/footer, cover page if needed
	5.	Save as your template.docx
Every future conversion will inherit all that formatting automatically.

Key “Looks Horrible” Problems This Solves



|Problem                |Fix                                            |
|-----------------------|-----------------------------------------------|
|Wrong fonts / sizes    |Template named styles override everything      |
|Inline CSS chaos       |Strip in Stage 1 before converting             |
|Broken table widths    |pandoc + `python-docx` post-fix with DXA widths|
|No TOC                 |`--toc` flag in pandoc                         |
|Ugly code blocks       |Map `<pre>` → `Source Code` style in template  |
|Missing headers/footers|Baked into your reference.docx                 |

Install

pip install beautifulsoup4 python-docx
# pandoc via winget, brew, or apt
winget install JohnMacFarlane.Pandoc


This gives you a repeatable, scriptable pipeline you can hand off to Windsurf or wire into a CI step. Want me to write the full end-to-end script?​​​​​​​​​​​​​​​​
