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

Development should work equally well on Linux, Windows (with or without
[WSL][]), or macOS.

[WSL]: https://docs.microsoft.com/en-us/windows/wsl/about

You'll need to have [Hugo][] installed as required for your operating system.
**Please note:** we use a pinned version of Hugo; if you need to check the
current version used for building, see the [Github Workflow][workflow].

[workflow]: ./.github/workflows/gh-pages.yaml

**Note:** Currently, madewhere requires Hugo "Extended" be installed; the
non-extended version will work for the local server, but test builds will fail.

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

For example, if you were adding a brand called "Cool Brand", you would do:

```shell
hugo new brands/cool-brand
```

…which will create a new file `brands/cool-brand/index.md` for you to edit.

Follow these rules when creating new content:

* Content file names should be `kebab-case`
* Content file names should be lowercase
* Content file names should be valid URLs; do not use special characters,
  accents, etc.
  * When replacing special characters, use a `-`; e.g. "D'Addario" becomes
    `d-addario`
  * Do not place multiple dashes next to one another: if replacing multiple
    characters, collapse them to a single character; e.g. "Puss 'n Boots"
    `puss-n-boots` _not_ `puss--n-boots`.
* Name files by the full brand name you are adding, but omit superfluous
  postfixes like "company" unless they are common in referring to the brand
* Content should be in a directory, to house any other files we might want to
  carry with it (images, etc.). The archetypes handle this automatically.
  * Exceptions are for meta content pages that are part of the site, such as the
    "About" page.
* Create all files as UTF-8, with Unix newlines
* Trim trailing whitespace
* Insert a final newline at the end of files

We provide an [editorconfig][] for automatically handling the last three bullets
if your editor supports this.

[editorconfig]: https://editorconfig.org/

## Markdown Style Guide

This content of this site is primarily written in Markdown, with yaml
frontmatter. We want to keep our markdown consistent and maintainable. When
possible we want to offload as much to the theme so that we don't have to write
unnecessary Markdown, with the added benefit that changes are pushed to all
existing pages. If you want to add a new feature, section, or the like, please
[open an issue][issues] to discuss further before implementing.

[issues]: ./issues/new

Our style guide for Markdown is as follows:

* Wrap lines at 80 characters
* Trim trailing spaces
* When writing lists:
  * Use `*` for bulleted lists
  * Use `1.` for numbered lists. All entries should be `1.`, unincremented. Let
    the processor handle incrementing for us.
  * Use two spaces for indentation
  * Visually indent line continuations under the previous line
* Leave a single empty line between paragraphs
* When writing headings:
  * Use `#` for all headings, not "dash" underlines
* When creating links:
  * Prefer named links to inline links; e.g. `[Link Text][link]`
  * When using named links, if the name is the same as the link, use trailing
    brackets; e.g. `[Link Text][]`
  * Use Hugo shortcodes for linking to other content; we don't want to manually
    manage internal links; e.g. `{{< ref "some-content-name" >}}`
* When custom styling is needed, implement a Hugo shortcode; an example within
  the codebase is the `admonishment` shortcode.
* When linking to commonly used URLs, prefer adding them either to the page or
  site's params, so they can be changed in one place. For examples, see usages
  of the `repository` param defined in [`config.yaml`][config]

[config]: ./config.yaml

Sadly, we can't autoformat markdown due to the parser in [Prettier][] failing
on Hugo's link refs; however if this changes or a workaround becomes available
(or we write one) we will just defer to Prettier's formatting most likely.

[prettier]: https://prettier.io

### Frontmatter

The yaml frontmatter that is auto-generated from the archetypes attempts to be
self-explanatory, but probably only half successfully; the rules are:

* Singular items (such as `parent`) are meant to be single values
* Plural items (such as `categories`) are meant to be list values

A description of the non-standard frontmatter is as follows; the rest follows
Hugo's [standard frontmatter][frontmatter].

[frontmatter]: https://gohugo.io/content-management/front-matter/

* `stub (boolean)`: when `true` the article is marked as being a "stub"; we use
  the same definition as wikipedia here, where a "stub" is a placeholder article
  which is not yet complete.
* `categories ([]string)`: an array of strings representing categories; this
  should match existing categories unless you are adding a new one
* `origins ([]string)`: an array of strings representing the origins; this
  should match existing origins unless you are adding a new one
* `tags ([]string)`: an array of strings representing free-form associative
  data, however some tags have special meaning, detailed below.
* `vendors ([]string)`: an array of strings of vendors who carry the brand's
  products; should be the identifier of the vendor, e.g. `/vendors/some-vendor`
  would mean a value of `some-vendor`
* `links ([]link)`: an array of links to external sites; more detail on `link`
  is below
* Parent data, which relates a brand to another parent brand. There are two ways
  to specify this relation, either as an internal or external link. You should
  do one or the other but never both:
  * `parentLink (link)`: a link to an external parent site
  * `parent`: an internal identifier of another brand; e.g. `/brands/some-brand`
    would mean a value of `some-brand`

#### Links

A `link` is just a special data type that we use in a few locations for both
configuration and frontmatter; it has two properties:

* `url (string)`: the full URL to use; e.g. `https://brand.example/`
* `text (string)`: the text to display on the anchor tag

### Tags

Tags are a freeform taxonomy for relating data; they can have their own pages
and descriptions (under `/content/tags`) but generally we don't want to add them
completely arbitrarily.

Some tags have a second purpose however, as they are used for broader "thing you
should note" sort of categories, and those may have an actual effect on the
brand page that's being rendered. Those tags are listed below:

* `mixed-origin`: Denotes a brand that doesn't make their products in any
  single country.
* `independent`: Denotes a brand with no parent corporation

## Theming, HTML

The site is built using the [Ananke][] theme, pinned to a specific version.
Under the hood, Ananke uses the [Tachyons][] CSS framework, which provides a
large number of utility classes for styling content. We do not have a custom CSS
build pipeline, so lean on these utility classes for styling your content.

Currently, we override parts of the Ananke theme as necessary, but lean on the
theme for the vast majority of the site.

Ideally some day we will write our own theme, but this is adequate for the
prototype.

Should you need to make any modifications, start by copy/pasting the template
from Ananke into the `/layouts` directory, in the appropriate location (same as
within the Ananke source) and then make your modifications as necessary. Note
that Ananke is MIT licensed, as is the code for madewhere.

We use [Font Awesome][] for icons, using those available in the free set, which
is CC-BY-4.0 licensed. However we re-host them to ensure all site content comes
from a single origin. We selectively include fonts as needed; see
[`site-icons.html`][site-icons] for how they are included. Ensure to add an
accessible title for any new icons added.

[Ananke]: https://github.com/theNewDynamic/gohugo-theme-ananke
[Tachyons]: https://tachyons.io/
[Font Awesome]: https://fontawesome.com/
[site-icons]: ./layouts/partials/site-icons.html

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

[Github Actions]: https://github.com/features/actions
[GitHub Pages]: https://pages.github.com/
