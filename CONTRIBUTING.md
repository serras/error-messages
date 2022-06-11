# Contributing to the Message Index

Thank you for your interest in contributing! This site is a project of
the [Haskell Foundation](http://haskell.foundation), so the
[Guidelines for Respectful Communication](https://haskell.foundation/guidelines-for-respectful-communication/)
are in force.

The message index is in the directory `message-index`.

## Building GHC with Error Codes

Please follow the instructions on [building GHC with Hadrian](https://gitlab.haskell.org/ghc/ghc/-/wikis/building/hadrian),
switching to the wip/T21684` branch before compilation.
Your error messages would then contain an ID.

```
$ _build/stage1/bin/ghc --interactive
GHCi, version 9.5.20220609: https://www.haskell.org/ghc/  :? for help
ghci> 1 + "foo"

<interactive>:1:1: error: [GHC-39999]
    • No instance for (Num String) arising from the literal '1'
    • In the first argument of '(+)', namely '1'
      In the expression: 1 + "foo"
      In an equation for 'it': it = 1 + "foo"
```

## Task Lists

We keep track of which errors are being worked on, and which still require documentation,
using a bunch of issues:

- [Type checker errors](https://github.com/haskell/error-messages/issues/66)
- [Driver errors](https://github.com/haskell/error-messages/issues/67)
- [Parser errors](https://github.com/haskell/error-messages/issues/68)
- [Desugarer errors](https://github.com/haskell/error-messages/issues/69)

## Contributing New Messages

The Haskell Message Index is generated from a collection of files on
disk using Hakyll. Inside the top-level of the site source, there is a
`messages` directory. Within `messages`, each subdirectory represents
a message whose name is the message code. This subdirectory contains a
file `index.md` that describes the message. Additionally,
subdirectories of the message directory may represent examples - each
example contains a file `index.md` as well as a number of Haskell
files that represent the example.

A message with ID `GHC-123` and two examples might have the following structure:

 * `/messages` - the root of all messages
   * `/messages/GHC-123` - data corresponding to message `GHC-123`
     * `/messages/GHC-123/index.md` - description and metadata for `GHC-123`
     * `/messages/GHC-123/example1/` - files related to the first example
     * `/messages/GHC-123/example1/index.md` - description and metadata for the first example
     * `/messages/GHC-123/example1/before/Main.hs` - an example file that exhibits the error
     * `/messages/GHC-123/example1/after/Main.hs` - an example file in which the error has been fixed
     * `/messages/GHC-123/example2/` - files related to the first example
     * `/messages/GHC-123/example2/index.md` - description and metadata for the second example
     * `/messages/GHC-123/example2/before/Main.hs` - an example file that exhibits the error
     * `/messages/GHC-123/example2/after/Main.hs` - an example file in which the error has been fixed

The path components `messages` and the two `index.md` files must be
named as specified here, while the other components may vary.

### Message Descriptions

Message descriptions (in `index.md` in the message directory) are
written in Markdown with Pandoc-style metadata blocks. Here's an
example message description:

````markdown
---
title: Unification Error
summary: Two types that should match are in conflict
introduced: 9.4.1
severity: error
---


A unification error occurs when the type checker has received conflicting expectations about an expression's type.


## Example Text

```
Unification error: Expected type A but got type B
```
````

The fields in the metadata block should be: 
 * `title` - a short title used for the page header and for links to the description
 * `summary` - a short summary used in the message index
 * `introduced` - the tool version in which the error code was introduced (optional)

### Example Descriptions
Example descriptions are written in Markdown with Pandoc-style
metadata, just like message descriptions. They have only the `title`
field. All `.hs` files are shown in the list of files for the
example. The `index.md` file should explain how the files illustrate
the message.


## Contributing to the Site

The site is generated using [Hakyll](https://jaspervdj.be/hakyll/).
Pull requests that make it easier to understand or navigate are very
welcome. The main generator `site.hs` is formatted using
[Ormolu](https://github.com/tweag/ormolu).
