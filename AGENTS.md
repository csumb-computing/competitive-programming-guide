# AGENTS.md

## Project

A notes site for competitive programming, built with [Hugo](https://gohugo.io)
and the [Hugo Book](https://themes.gohugo.io/themes/hugo-book/) theme, deployed
to GitHub Pages at
<https://csumb-computing.github.io/competitive-programming-guide/>.

The site teaches common operations side by side in Python and C++.

## Commands

| Task | Command |
| --- | --- |
| Local preview (rebuilds on edit) | `hugo server` → <http://localhost:1313/> |
| Build the site | `hugo` (output in `public/`) |
| Build the way CI does | `hugo --minify` |

Hugo v0.158 or newer is required (the theme's `min_version`). CI pins `0.166.0`.
The extended edition and Dart Sass are not required.

There is no test suite. Validate changes by building with `hugo --minify` and
confirming it completes without warnings.

## Layout

- `content/` — all Markdown content. Each top-level folder is a section that
  appears in the sidebar menu.
  - `content/explanations/` — conceptual explanations (e.g. undefined behavior).
  - `content/how to/` — task-oriented recipes. Note the space in the folder name.
  - `content/other/` — tooling and templates.
- `content/_index.md` — the home page.
- `assets/` — images (`cppaste.png`) and `assets/styles/custom.css`.
- `themes/hugo-book/` — the theme, vendored as a git submodule at v0.15.0.
- `hugo.yaml` — site configuration.
- `.github/workflows/github-pages.yaml` — build and deploy workflow.

`public/`, `resources/`, and `.hugo_build.lock` are generated and gitignored.
Never commit build output.

## Content conventions

These are the patterns every page follows. Match them when adding or editing
pages.

- **One page per file.** Each page sets its `title` in front matter, matching the
  H1. The file name is the URL slug, so use Title Case with spaces
  (`Sort a list.md`, `Find index of min or max.md`).
- **Start with an H1** that matches the page title, e.g. `# Sort a list`.
- **Organize by language.** Most pages have a `## Python` section followed by a
  `## C++` section, in that order, covering the same operation in parallel.
  Group variants with `##`/`###` when a page has more than one form (e.g.
  `## With Scalar` / `## With List`, or `### Method 1`).
- **Fence code blocks with a language tag**: `python`, `c++`, `bash`, `sh`,
  `javascript`, `yaml`.
- **Annotate results in comments** so the reader sees the output, e.g.
  `sorted([3, 1, 2]) // [1, 2, 3], returns a NEW list`.
- **Link to the official docs** inline (python.org, cppreference.com) when
  introducing a function.
- **Call out edge cases.** Say what happens on empty input, and contrast
  Python's exceptions with C++'s undefined behavior. Use a `#### Python Errors`
  subheading when documenting exceptions.
- **Cross-reference related pages** with relative Markdown links such as
  `[cptest](./cptest.md)`. The theme resolves these to Hugo URLs
  (`BookPortableLinks: warning` in `hugo.yaml`), and warns when a target is
  missing.

Keep prose concise and in the second person ("you"), and explain *why* a
technique is recommended, not just how.

## Git and CI

- Commit messages are short, sentence case, and imperative
  (`Fix typos`, `Rename how-to directory and add other notes`).
- The workflow builds on every push and pull request, and deploys only from
  `main`. CI checks out submodules recursively, so the theme must stay a
  submodule.
