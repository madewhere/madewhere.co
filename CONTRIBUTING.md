# Contributing

Thanks for your interest in contributing!

This document covers the more technical aspects of contributing. If you haven't
already, be sure to read our [Code of Conduct](./CODE_OF_CONDUCT.md) as it
details what we expect from our contributors; following it is a requirement of
contributing to this project.

This guide also assumes some familiarity with [Hugo][], the popular static site
framework. If you aren't familiar, please read its documentation as we won't
reproduce much of it here.

[hugo]: https://gohugo.io/

## Setup

Development should work equally well on Linux, Windows (with or without [WSL]),
or macOS.

You'll need to have [Hugo] installed as required for your operating system.
**Please note:** we use a pinned version of Hugo; if you need to check the
current version used for building, see the [Github Workflow][workflow].

[workflow]: ./.github/workflows/gh-pages.yaml

If you need a different version of Hugo installed; it's a portable binary and
keeping a different version installed is as easy as having it available in your
path.

## Creating new Entries

We offer Hugo archetypes for all major content types; rely on those for creating
new content entries:

```shell
# create a new brand
hugo new brands/<brand-name>
# create a new vendor
hugo new vendors/<vendor-name>
```

…the above follows for origins, tags, and categories.

Follow these rules when creating new content:

- Content file names should be `kebab-case`
- Content file names should be lowercase
- Content file names should be valid URLs; do not use special characters,
  accents, etc.
- Name files by the full brand name you are adding, but omit superfluous
  postfixes like "company" unless they are common in referring to the brand
- Content should be in a directory, to house any other files we might want to
  carry with it (images, etc.). The archetypes handle this automatically.
  - Exceptions are for meta content pages that are part of the site, such as the
    "About" page.

## Editor Configuration

We provide an out-of-the-box recommended configuration for [Visual Studio
Code][vscode], and that is our recommended editor for working on content.

Please install the recommended extensions, and you should get formatting out of
the box which matches our style guide.

All files are expected to be formatted by [prettier][] before commit, regardless
of your environment; this includes:

- Markdown
- Yaml
- HTML
- CSS

[prettier]: https://prettier.io/

## Markdown Style Guide

This content of this site is primarily written in Markdown, with yaml
frontmatter. We want to keep our markdown consistent and maintainable. When
possible we want to offload as much to the theme so that we don't have to write
unnecessary Markdown, with the added benefit that changes are pushed to all
existing pages. If you want to add a new feature, section, or the like, please
[open an issue][issues] to discuss further before implementing.

[issues]: ./issues/new

Generally: we use `prettier` to format our Markdown, and we use the default
settings save one: forcing lines to be wrapped at 80 characters. If your editor
supports it, we'd recommend using "format on save" to run prettier
automatically, and you can completely avoid thinking about these issues.

Our style guide for Markdown is as follows:

- Wrap lines at 80 characters
- Trim trailing spaces
- When writing lists:
  - Use `-` for bulleted lists
  - Use `1.` for numbered lists. All entries should be `1.`, un-incremented. Let
    the processor handle incrementing for us.
  - Use two spaces for indentation
  - Visually indent line continuations under the previous line
- Leave a single empty line between paragraphs
- When writing headings:
  - Use `#` for all headings, not "dash" underlines
- When creating links:
  - Prefer named links to inline links; e.g. `[Link Text][link]`
  - When using named links, if the name is the same as the link, use trailing
    brackets; e.g. `[Link Text][]`
  - Use Hugo shortcodes for linking to other content; we don't want to manually
    manage internal links; e.g. `{{< ref "some-content-name" >}}`
- When custom styling is needed, implement a Hugo shortcode; an example within
  the codebase is the `admonishment` shortcode.
- When linking to commonly used URLs, prefer adding them either to the page or
  site's params, so they can be changed in one place. For examples, see usages
  of the `repository` param defined in [`config.yaml`][config]

[config]: ./config.yaml

## Theming, HTML

The site is built using the [Ananke][] theme, pinned to a specific version.
Under the hood, Ananke uses the [Tachyons][] CSS framework, which provides a
large number of utility classes for styling content. We do not have a custom CSS
build pipeline, so lean on these utility classes for styling your content.

Currently, we override parts of the Ananke theme as necessary, but lean on the
theme for the vast majority of the site.

Ideally some day we will write our own theme, but this is adequate for the
prototype.

[ananke]: https://github.com/theNewDynamic/gohugo-theme-ananke
[tachyons]: https://tachyons.io/

## Build Process

It's our goal to keep the build process as simple as possible. Should more
complex needs arise we can re-evaluate, but the goal is to just use Hugo
directly without any additional build tools.

Regardless, it's extremely important that the build be possible on Linux,
Windows (with or without WSL), and macOS. That's the one requirement we are
unwilling to change.

The build process is handled entirely within [GitHub Actions][], and hosting is
within [GitHub Pages][]. The build and deploy happens automatically via Actions,
causing the updated site to go live within minutes. See the [workflow][] for
further details.

[github actions]: https://github.com/features/actions
[github pages]: https://pages.github.com/
