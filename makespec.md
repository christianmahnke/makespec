# Introduction

{ABSTRACT}

# Usage

## Setup

Best practice using makedoc is to host your specification in a git repository,
optionally published at [GitHub](http://github.com/). Your repository should
contain at least:

 * The specification as Pandoc Markdown source file (e.g. `myspec.md`)
 * A `Makefile` with basic settings and [configuration], such as:
   
        NAME=myspec
        GITHUB=https://github.com/myaccount/myspec/
     
        include makespec/Makefile

 * A subdirectory `makespec` containing makespec. Best practice is inclusion
   as as git submodule. To do so in a new git repository:

        git submodule add https://github.com/jakobib/makespec.git

To clone an existing specification that uses makespace this way:

    git clone --recursive http://github.com/myaccount/myspec.git

If you publish the specification as GitHub pages, you should not forget to also
clone the `gh-pages` branch:

    git checkout -b gh-pages origin/gh-pages && git checkout master

## Workflow

Make sure you have the most recent version

    git pull origin master gh-pages

Edit the specification source file in Markdown syntax, for instance with vim
editor

    vim myspec.md

Create a HTML version

    make html

Commit to your repository

    git add Makefile myspec.md
    git commit -m "improved my fancy specification"

Create a `gh-pages` branch with the HTML version

    make website

Publish

    git push origin master gh-pages

## Configuration

[configuration]: #configuration

### Basic metadata

NAME
  : Required short name. Should not contain spaces and similar nasty characters.

SOURCE
  : Source file in Pandoc Markdown syntax, set to `NAME.md` by default.

GITHUB
  : Github repository to link to in revision history.

TITLE
  : Title, unless already specified in the source file.

AUTHOR
  : List of authors, unless already specified in the source file.

DATE
  : Fixed date of publication. Set to a timestamp of the latest commit
    by default.

ABSTRACT
  : A short abstract (in Markdown syntax) which is used as template 
    variable ABSTRACT.

ABSTRACT_FROM
  : A file to read abstract from if no ABSTRACT was defined. Set to
    `abstract.md` by default.

### Output control

REVISIONS
  : Number of revisions to show in the revision history (GIT_CHANGES).

FORMATS
  : If your specification contains a RDF ontology written in Turtle syntax,
    set `FORMATS=ttl owl`. More formats may be supported in the future.
    Format `html` is always enabled by default.

HTML_TEMPLATE
  : An optional Pandoc template for HTML output

HTML_TEMPLATE
  : An optional CSS file for HTML output

TEX_TEMPLATE
  : An optional Pandoc template for LaTeX and PDF output

## Document variables

The following variables, if enclosed in curly brackets (such as
`{THIS_VARIABLE}`) are automatically replaced before conversion from Markdown
syntax.

GIT_REVISION_DATE
  : timestamp of the latest commit.

GIT_REVISION_HASH
  : Short revision hash of the latest commit.

GIT_CHANGES
  : Revision history. Length can be set with configuration variable `REVISIONS`.

GIT_ATOM_FEED
  : URL of an Atom feed with revisions at GitHub.

ABSTRACT
  : Abstract, if defined with configuration variable `ABSTRACT` or 
    `ABSTRACT_FROM`.

VERSION
  : The current version number as determined by looking for the latest git tag
    in the current branch that matches the regular expression `^v[0-9]`.

## Plugins

`plugins.md`{.include}

## Requirements

* GNU Make
* Perl >= 5.14.1
* [Pandoc](http://johnmacfarlane.net/pandoc/) version >= 1.9
* [Rapper](http://librdf.org/raptor/rapper.html) from Raptor RDF library
  (only if writing an RDF ontology)

# Examples

The following specifications make use of makespec:

* [Simple Service Status Ontology (SSSO)](https://github.com/gbv/ssso)
* [Document Service Ontology (DSO)](https://github.com/gbv/dso)
* [Document Availability Information API (DAIA)](https://github.com/gbv/daiaspec)
* [Patrons Account Information API (PAIA)](https://github.com/gbv/paia)
* ...

Last but not least, the documentation of makespec is also created with makespec.
[This document](https://github.com/jakobib/makespec/blob/master/README.md) was
last modified at {GIT_REVISION_DATE} with hash {GIT_REVISION_HASH}.

# Revision history

This document is version {VERSION}.

Also available as [Atom feed]({GIT_ATOM_FEED}).

{GIT_CHANGES}
