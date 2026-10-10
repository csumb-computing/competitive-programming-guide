# Competitive Programming

A notes site built with [Hugo](https://gohugo.io) and the
[Hugo Book](https://themes.gohugo.io/themes/hugo-book/) theme.

## Requirements

- Hugo v0.158 or newer. The extended edition and Dart Sass are **not** required
  (the theme dropped the SASS dependency in v0.15.0).

## Local development

```sh
hugo server
```

Then open <http://localhost:1313/>. The server rebuilds automatically as you edit.

## Build

```sh
hugo
```

The generated site is written to `public/`.

## Content

Content lives in `content/`. Each top-level folder is a section that shows up in
the sidebar menu.

- `content/how-to-basics/` — common operations in Python and C++.

To add a page, drop a Markdown file into the relevant section folder. The page
title is taken from the file name unless you add a `title` in front matter.

## Theme

The theme is vendored in `themes/hugo-book` at v0.15.0. To update it, replace the
folder with a fresh clone of the desired release:

```sh
rm -rf themes/hugo-book
git clone --depth 1 --branch v0.15.0 https://github.com/alex-shpak/hugo-book themes/hugo-book
```
