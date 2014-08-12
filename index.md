---
layout: default
---

<h1 class="hide">{{ site.title }}</h1>
<h2 class="alpha  site-title">{{ site.description }}</h2>

## About the Author

<cite>CSS Guidelines</cite> is a document by me, [Harry
Roberts](http://csswizardry.com/work/). I am a Consultant Front-end Architect
from the UK, and I help companies all over the world write and manage better
quality UIs for their products and teams. I am available for hire.

<p class="text-center">
<a href="https://twitter.com/csswizardry" class="btn  btn--secondary"><span class="hide-palm">Follow me on </span>Twitter</a>
or <a href="http://csswizardry.com/work/" class="btn">Hire<span class="hide-palm"> Me</span></a>
</p>

---

## Buy the Guidelines

<cite>CSS Guidelines</cite> is provided through a pay-what-you-like model—from
$0 upward. If <cite>CSS Guidelines</cite> is useful to you or your team, please
consider [supporting it](https://gumroad.com/l/JAgjq).

<p class="text-center">
<a href="https://gumroad.com/l/JAgjq" class="btn">Buy the Guidelines</a>
</p>

---

## Contents

* [Introduction](#introduction)
* [Syntax and Formatting](#syntax-and-formatting)
    * [HTML](#html)

---

## Introduction

CSS is not a pretty language: for all it is simple to learn and get started
with, it soon becomes problematic at any reasonable scale. There isn’t much we
can do to change how CSS works, but we can make changes to the way we author and
structure it.

In working on large, long-running projects, with dozens of developers of
different specialisms and abilities, it is important that we all work in a
unified way in order to—among other things—

* keep stylesheets maintainable.
* keep code transparent, sane, and readable.
* keep stylesheets scalable.

There are a variety of techniques we must employ in order to satisfy these
goals, and <cite>CSS Guidelines</cite> is a document of recommendations and
approaches that will help us to do so.

### Importance of a Styleguide

A coding styleguide—note, not a visual styleguide—is a valuable tool for teams
who

* build and maintain products for a reasonable length of time.
* have developers of differing abilities and specialisms.
* have a number of different developers working on a product at any given time.
* on-board new staff regularly.
* have a number of codebases that developers dip in and out of.

Whilst styleguides are typically more suited to product teams—large codebases on
long-lived and evolving projects, with multiple developers contributing over
prolonged periods of time—all developers should strive for a degree of
standardisation in their code.

A good styleguide, when well followed, will

* set the standard for code quality across a codebase.
* promote consistency across codebases.
* give developers a feeling of familiarity across codebases.
* increase productivity.

Styleguides should be learned, understood, and implemented at all times on a
project which is governed by one, and any deviation must be fully justified.

<cite>CSS Guidelines</cite> is *a* styleguide; it is not *the* styleguide. It
contains methodologies, techniques, and tips that I would firmly recommend to my
clients and teams, but your own tastes and circumstances may well be different.
Your mileage may vary.

---

## Syntax and Formatting

One of the simplest forms of a styleguide is a set of rules regarding syntax and
formatting. Having a standard way of writing (_literally_ writing) CSS means
that code will always look and feel familiar to all members of the team.

Further, code that looks clean _feels_ clean. It is a much nicer environment to
work in, and prompts other team members to maintain the standard of cleanliness
that they found. Ugly code sets a bad precedent.

At a very high-level, we want:

* Four (4) space indents. No tabs.
* 80 character wide columns
* Multi-line CSS.
* Meaningful use of whitespace.

### Multiple Files

With the meteoric rise of preprocessors of late, more often is the case that
developers are splitting CSS across multiple files.

Even if not using a preprocessor, it is a good idea to split discrete chunks of
code into their own files, which are concatenated during a build step.

If, for whatever reason, you are not working across multiple files, the next
sections might require some bending to fit your setup.

### Table of Contents

A table of contents is a fairly substantial maintenance overhead, but the
benefits it brings far outweigh any costs. It takes a diligent developer to keep
a table of contents up to date, but it is well worth sticking with. An
up-to-date table of contents provides a team with a single, canonical catalogue
of what is in a CSS project, what it does, and in what order.  

A simple table of contents will—in order, naturally—simply provide the name of
the section and a brief summary of what it is and does, for example:

    /**
     * CONTENTS
     *
     * SETTINGS
     * Global...............Globally-available variables and config.
     *
     * TOOLS
     * Mixins...............Useful mixins.
     *
     * GENERIC
     * Normalize.css........A level playing field.
     * Box-sizing...........Better default `box-sizing`.
     *
     * BASE
     * Headings.............H1–H6 styles.
     *
     * OBJECTS
     * Wrappers.............Wrapping and constraining elements.
     *
     * COMPONENTS
     * Page-head............The main page header.
     * Page-foot............The main page footer.
     * Buttons..............Button elements.
     *
     * TRUMPS
     * Text.................Text helpers.
     */

Each item maps to a section and/or include.

Naturally, this section would be substantially larger on the majority of
projects, but hopefully we can see how this section—in the master
stylesheet—provides developers with a project-wide view of what is being used
where, and why.

### 80 Characters Wide

Where possible, limit CSS files’ width to 80 characters. Reasons for this
include

* the ability to have multiple files open side by side.
* viewing CSS on sites like GitHub, or in terminal windows.
* providing a comfortable line length for comments.

<pre><code>/**
 * I am a long-form comment. I describe, in detail, the CSS that follows. I am
 * such a long comment that I easily break the 80 cahracter limit, so I am
 * broken across several lines.
 */</code></pre>

There will be unavoidable exceptions to this rule—like URLs or gradient
syntax—which shouldn’t be worried about.

### Titling

Begin every new major section of a CSS project with a title:

    /*------------------------------------*\
        #SECTION-TITLE
    \*------------------------------------*/

    .selector {
    }

The title of the section is prefixed with a hash (`#`) symbol to allow us to
perform more targeted searches (e.g. `grep`, etc.): instead of searching for
just <kbd>SECTION-TITLE</kbd>—which may yield many results—a more scoped search
of <kbd>#SECTION-TITLE</kbd> should return only the section in question.

Leave a carriage return between this title and the next line of code (be that a
comment, some Sass, or some CSS).

If you are working on a project where each section is its own file, this title
should appear at the top of each one. If you are working on a project with
multiple sections per file, each title should be preceded by five (5) carriage
returns. This extra whitespace coupled with a title makes new sections much
easier to spot when scrolling through large files:

    /*------------------------------------*\
        #A-SECTION
    \*------------------------------------*/

    .selector {
    }





    /*------------------------------------*\
        #ANOTHER-SECTION
    \*------------------------------------*/

    /**
     * Comment
     */

    .another-selector {
    }

### Anatomy of Rulesets

Before we discuss how we write out our rulesets, let’s first familiarise
ourselves with the relevant terminology:

    [selector] {
        [property]: [value];
        [<--declaration--->]
    }

For example:

    .foo, .foo--bar,
    .baz {
        display: block;
        background-color: green;
        color: red;
    }

Here you can see we have

* related selectors on the same line; unrelated selectors on new lines.
* a space before our opening brace (`{`).
* properties and values on the same line.
* a space after our property–value delimiting colon (`:`).
* each declaration on its own new line.
* the opening brace (`{`) on the same line as our last selector.
* our first declaration on a new line after our opening brace (`{`).
* our closing brace (`}`) on its own new line.
* each declaration indented by four (4) spaces.
* a trailing semi-colon (`;`) on our last declaration.

This format seems to be the largely universal standard (except for variations in
number of spaces, with a lot of developers preferring two (2)).

As such, the following would be incorrect:

    .foo, .foo--bar, .baz
    {
    	display:block;
    	background-color:green;
    	color:red }

Problems here include

* tabs instead of spaces.
* unrelated selectors on the same line.
* the opening brace (`{`) on its own line.
* the closing brace (`}`) does not sit on its own line.
* the trailing (and, admittedly, optional) semi-colon (`;`) is missing.
* no spaces after colons (`:`).

### Multi-line CSS

CSS should be written across multiple lines, except in very specific
circumstances. There are a number of benefits to this:

* A reduced change of merge conflicts, because each piece of functionality
  exists on its own line.
* More ‘truthful’ and reliable `diff`s, because one line only ever carries one
  change.

Exceptions to this rule should be fairly apparent, such as similar rulesets that
only carry one declaration each, for example:

    .icon {
        display: inline-block;
        width:  16px;
        height: 16px;
        background-image: url(/img/sprite.svg);
    }

    .icon--home     { background-position:   0     0  ; }
    .icon--person   { background-position: -16px   0  ; }
    .icon--files    { background-position:   0   -16px; }
    .icon--settings { background-position: -16px -16px; }

These types of ruleset benefit from being single-lined because

* they still conform to the one-reason-to-change-per-line rule.
* they share enough similarities that they don’t need to be read as thoroughly
  as other rulesets—there is more benefit in being able to scan their selectors,
  which are of more interest to us in these cases.

### Indenting

As well as intending individual declarations, indent entire related rulesets to
signal their relation to one another, for example:

    .foo {
    }

        .foo__bar {
        }

            .foo__baz {
            }

By doing this, a developer can see at a glance that `.foo__baz {}` lives inside
`.foo__bar {}` lives inside `.foo {}`.

This quasi-replication of the DOM tells developers a lot about where classes are
expected to be used without them having to refer to a snippet of HTML.

#### Indenting Sass

Sass provides nesting functionality. That is to say, by writing this:

    .foo {

        .bar {
        }

    }

…we will be left with this compiled CSS:

    .foo {}
    .foo .bar {}

When indenting Sass, we stick to the same four (4) spaces, and we also leave a
blank line before and after the nested ruleset.

**N.B.** Nesting in Sass should be avoided wherever possible. See [[section]]
for more details.

#### Alignment

Attempt to align common and related identical strings in declarations, for
example:

    .foo {
        -webkit-border-radius: 3px;
           -moz-border-radius: 3px;
                border-radius: 3px;
    }

    .bar {
        position: absolute;
        top:    0;
        right:  0;
        bottom: 0;
        left:   0;
        margin-right: -10px;
        margin-left:  -10px;
        padding-right: 10px;
        padding-left:  10px;
    }

This makes life a little easier for developers whose text editors support column
editing, allowing them to change several identical and aligned lines in one go.

### Meaningful Whitespace

As well as indentation, we can provide a lot of information through liberal and
judicious use of whitespace between rulesets. We use:

* One (1) empty line between closely related rulesets.
* Two (2) empty lines between loosely related rulesets.
* Five (5) empty lines between entirely new sections.

For example:

    /*------------------------------------*\
        #FOO
    \*------------------------------------*/

    .foo {
    }

        .foo__bar {
        }


    .foo--baz {
    }





    /*------------------------------------*\
        #BAR
    \*------------------------------------*/

    .bar {
    }

        .bar__baz {
        }

        .bar__foo {
        }

There should never be a scenario in which two rulesets do not have an empty line
between them. This would be incorrect:

    .foo {
    }
        .foo__bar {
        }
    .foo--baz {
    }

### HTML

Separate thematic chunks of markup with a blank line.

<!--

---

## Naming Conventions

Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac
turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor
sit amet, ante. Donec eu libero sit amet quam egestas semper. Aenean ultricies
mi vitae est. Mauris placerat eleifend leo.

---

## CSS Selectors

Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac
turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor
sit amet, ante. Donec eu libero sit amet quam egestas semper. Aenean ultricies
mi vitae est. Mauris placerat eleifend leo.

### Specificity

Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac
turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor
sit amet, ante. Donec eu libero sit amet quam egestas semper. Aenean ultricies
mi vitae est. Mauris placerat eleifend leo.

---

## Architecture

Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac
turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor
sit amet, ante. Donec eu libero sit amet quam egestas semper. Aenean ultricies
mi vitae est. Mauris placerat eleifend leo.

---

## Layout

-->
