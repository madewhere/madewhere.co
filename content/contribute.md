---
title: Contributing
description: Contributing listings to this site.
date: 2022-01-22
---

Thanks for your interest in contributing to our growing list of goods! Anyone is
allowed to contribute, following the guidelines in this document.

First of all, contributors must follow our [Code of Conduct][].

[code of conduct]: {{% param "codeOfConduct.url" %}}

Second, contributions to this site happen on [GitHub][]; if you don't have an
account there, you'll want to create one. Github is a website where people
collaborate on code; but if you're not a programmer, don't worry! You can add to
the site in a number of ways, and it doesn't have to involve writing code if
that's not your thing.

[github]: https://github.com/

Third, remember that the people who run this site are volunteers, and aren't
paid for their participation. It might take some time to get to your
contribution, and we might ask you for more information, for changes to be made,
or we could even reject your contribution with reason. Please be patient and
kind!

Fourth, understand that any contributions you make will be licensed under
Creative Commons licensing; you may view this license at [{{% param
"contentLicense.text" %}}][license], but the short of it is: your content
is yours, but anyone may reproduce it so long as it is attributed to this site.

[license]: {{% param "contentLicense.url" %}}

This contribution guide is split into two sections; the first is for everyone.
If you are comfortable with code and GitHub; you can [skip to the next
section]({{< ref "#code" >}}).

# Contribute by filing an Issue {#issue}

We maintain a list of [issues][] on our GitHub [repository][], which allow us to
track tasks among the site's contributors. If you'd like to add something, make
a correction, or just have a general suggestion for the site, you can file an
issue using the links below. When doing so, you'll be asked what you'd like to
add, and be given a template which can be filled out and submitted. Once you do,
our volunteers will triage it, discuss it with you, and if all goes well get
your contribution on the site.

**It's important to remember** that the people that maintain this site are
volunteers, and they aren't paid! It might take some time before you get a
response to your issue.

To file an issue, please click one of the following links:

* [Add a new brand or vendor][add-content]
* [Update an existing brand or vendor][update-content]
* [Update other site content not vendor or brand specific][meta-content]

[issues]: {{% param "repository.url" %}}/issues
[repository]: {{% param "repository.url" %}}
[file an issue]: {{% param "repository.url" %}}/issues/new

[add-content]: {{% param "repository.url" %}}/issues/new?assignees=fardog&labels=enhancement&template=NEW-CONTENT.yml&title=%5BNew+Content%5D%3A+
[update-content]: {{% param "repository.url" %}}/issues/new?assignees=fardog&labels=enhancement&template=UPDATE-CONTENT.yml&title=%5BUpdate+Content%5D%3A+
[meta-content]: {{% param "repository.url" %}}/issues/new?assignees=fardog&labels=enhancement&template=UPDATE-META.yml&title=%5BUpdate+Meta%5D%3A+

# Contributing via Pull Request {#code}

madewhere is built with [Hugo][], and its [repository][] is on GitHub.
Please see the [contribution guide][] there, which details getting your
environment set up (it's kept intentionally simple), adding new content, our
style guide, and hopefully everything else you need to get started!

[hugo]: https://gohugo.io
[contribution guide]: {{% param "contributing.url" %}}
