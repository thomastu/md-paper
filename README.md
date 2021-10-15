# Motivation

When I went back to school for a secondary degree, I found that the state of document management and generation in academia was sorely lacking some key workflows I depended on in my day-to-day job as a developer.  I set out to create a package that would be suitable for writing long-form papers meant for distribution and consumption in an academic context, but had all the advantages of plain-text based systems (version control, simplicity, portability.)  Similarly, there were a suite of features commonly found in rich document editors that plain text had no defacto solution for - namely reference management and labeling.  The end goal of this package is to provide an easy to way to convert a collection of markdown files into a single document with support for bibliographies, labeling and multi-format outputs.  This is based primarily on the following tools:

- pandoc
- pandoc-crossref
- citeproc

## Quickstart

1. Install the `mdpaper` package: `pip install mdpaper` and ensure you have `pandoc-crossref` installed.
2. Configure your document by creating a `settings.toml` file in the root directory of your project.

```toml
[mdpaper]
references="references.bib"

# Order matters, and content will be compiled in the order provided in this list.
index = [
    "coverpage.md",
    "src/*.md"
]
# Extensions are generated automatically
output="my-output-file-{date}"

# For .docx outputs, you can provide a reference document for styling rules and pages
template_docx="/path/to/reference/document.docx"

# Configure whether to include a ToC
toc=true
toc_depth=3

# Extra pandoc filters you wish to run
# This package will come with one named `pandoc-docxtras` which will provide
# \newpage and a custom \toc command
# Using \toc from this package is incompatible with the `toc` flag.
pandoc_filters=[
    "pandoc-docxtras"
]
```

3.  Run `md-paper`: `md-paper docx` or `md-paper pdf`