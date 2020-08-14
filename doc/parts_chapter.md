# Parts & Chapter

The `parts & chapters` listing approach in `_toc.yml`

## General Comments

This structure works pretty well when specifying books. The only issue is on the `html` side
and numbering is restarted in each `part` as there are two separate `toctree` entries into
the Sphinx AST. As section numbering is handeled by LaTeX in the `TeX` side the numbering
with this approach is fine for the `bookpattern` to be used (i.e. continuous chapters through
the parts)

**General Issues:**

- [HTML] Section numbers are reset for each `part` in `html`
- [LATEX] All chapters are contained in `Part 1` and parts don't feature in `latex`

## jupyterbook

The following `_toc.yml`:

```yaml
- file: intro
  numbered: true

- part: part1
  chapters:
  - file: part1/chapter1
  - file: part1/chapter2

- part: part2
  chapters:
  - file: part2/chapter1
    sections:
      - file: part2/chapter1-section1
      - file: part2/chapter1-section2
```

produces [html](https://htmlpreview.github.io/?https://github.com/mmcky/ebp-test-projectstructure/blob/master/parts_chapters/jupyterbook/_build/html/intro.html) and [pdf](https://github.com/mmcky/ebp-test-projectstructure/blob/master/parts_chapters/jupyterbook/_build/latex/book.pdf).

**Sphinx AST:**

```xml
<document source="/Users/matthewmckay/repos-collab/ebp-test-projectstructure/parts_chapters/jupyterbook/intro.md">
    <section ids="intro" names="intro">
        <title>
            Intro
        <paragraph>
            This is the intro
        <compound classes="toctree-wrapper">
            <toctree caption="part1" entries="(None,\ 'part1/chapter1') (None,\ 'part1/chapter2')" glob="False" hidden="True" includefiles="part1/chapter1 part1/chapter2" includehidden="False" maxdepth="-1" numbered="999" parent="intro" rawcaption="part1" rawentries="" titlesonly="True">
        <compound classes="toctree-wrapper">
            <toctree caption="part2" entries="(None,\ 'part2/chapter1')" glob="False" hidden="True" includefiles="part2/chapter1" includehidden="False" maxdepth="-1" numbered="999" parent="intro" rawcaption="part2" rawentries="" titlesonly="True">
```

## bookpattern

The following `_toc.yml` produces:

```yaml
- file: intro
  numbered: true

- part: part1
  chapters:
  - file: part1/chapter1
  - file: part1/chapter2

- part: part2
  chapters:
  - file: part2/chapter3
    sections:
      - file: part2/chapter3-section1
      - file: part2/chapter3-section2
```

with [html](https://htmlpreview.github.io/?https://github.com/mmcky/ebp-test-projectstructure/blob/master/parts_chapters/bookpattern/_build/html/intro.html) and [pdf](https://github.com/mmcky/ebp-test-projectstructure/blob/master/parts_chapters/bookpattern/_build/latex/book.pdf).

**Sphinx AST:**

A `toctree` is added to the end of the `chapter1` document which causes issues with `numbering`.

```xml
<document source="/Users/matthewmckay/repos-collab/ebp-test-projectstructure/parts_chapters/bookpattern/intro.md">
    <section ids="introduction" names="introduction">
        <title>
            Introduction
        <paragraph>
            This is the introduction
        <compound classes="toctree-wrapper">
            <toctree caption="part1" entries="(None,\ 'part1/chapter1') (None,\ 'part1/chapter2')" glob="False" hidden="True" includefiles="part1/chapter1 part1/chapter2" includehidden="False" maxdepth="-1" numbered="999" parent="intro" rawcaption="part1" rawentries="" titlesonly="True">
        <compound classes="toctree-wrapper">
            <toctree caption="part2" entries="(None,\ 'part2/chapter3')" glob="False" hidden="True" includefiles="part2/chapter3" includehidden="False" maxdepth="-1" numbered="999" parent="intro" rawcaption="part2" rawentries="" titlesonly="True">

```



