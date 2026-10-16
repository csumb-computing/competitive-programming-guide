# Competitive Programming

A notes site built with [Hugo](https://gohugo.io) and the
[Hugo Book](https://themes.gohugo.io/themes/hugo-book/) theme.

## Requirements

- Hugo v0.158 or newer. The extended edition and Dart Sass are **not** required
  (the theme dropped the SASS dependency in v0.15.0).

## Local development

Clone the repository together with its submodules:

```sh
git clone --recurse-submodules git@github.com:csumb-computing/competitive-programming-guide.git
```

If you already cloned without them, populate the submodules afterwards:

```sh
git submodule update --init --recursive
```

Then start the server:

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

- `content/explanations/` — conceptual explanations.
- `content/how to/` — common operations in Python and C++. Note the space in the
  folder name.
- `content/other/` — tooling and templates.

To add a page, drop a Markdown file into the relevant section folder and set its
`title` in front matter. The file name becomes the URL slug.

## Theme

The theme is a [git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules)
at `themes/hugo-book`, pinned to v0.15.0. Because it is a submodule, a plain
`git clone` leaves the folder empty — use `--recurse-submodules` (or run
`git submodule update --init --recursive` afterwards) to populate it. CI checks
out submodules recursively as well.

To update the theme to a new release, check out the tag inside the submodule and
commit the new gitlink:

```sh
cd themes/hugo-book
git fetch --tags
git checkout v0.15.0
cd ../..
git add themes/hugo-book
git commit -m "Update hugo-book to v0.15.0"
```
