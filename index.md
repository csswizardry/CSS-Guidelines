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

## Support the Guidelines

<cite>CSS Guidelines</cite> is provided through a pay-what-you-like model—from
$0 upward. If <cite>CSS Guidelines</cite> is useful to you or your team, please
consider [supporting it](https://gumroad.com/l/JAgjq).

<p class="text-center">
<a href="https://gumroad.com/l/JAgjq" class="btn">Support the Guidelines</a>
</p>

Get updates about changes, additions, and new and upcoming sections by following
[@cssguidelines](https://twitter.com/cssguidelines) on Twitter.

---

## Contents

* [Introduction](#introduction)
    * [The Importance of a Styleguide](#the-importance-of-a-styleguide)
    * [Disclaimers](#disclaimers)
* [Syntax and Formatting](#syntax-and-formatting)
    * [Multiple Files](#multiple-files)
    * [Table of Contents](#table-of-contents)
    * [80 Characters Wide](#characters-wide)
    * [Titling](#titling)
    * [Anatomy of a Ruleset](#anatomy-of-a-ruleset)
    * [Multi-line CSS](#multi-line-css)
    * [Indenting](#indenting)
        * [Indenting Sass](#indenting-sass)
        * [Alignment](#alignment)
    * [Meaningful Whitespace](#meaningful-whitespace)
    * [HTML](#html)
* [Commenting](#commenting)
    * [High-level](#high-level)
        * [Object–Extension Pointers](#objectextension-pointers)
    * [Low-level](#low-level)
    * [Preprocessor Comments](#preprocessor-comments)
    * [Removing Comments](#removing-comments)
* [Naming Conventions](#naming-conventions)
    * [Hyphen Delimited](#hyphen-delimited)
    * [BEM-like Naming](#bem-like-naming)
        * [Starting Context](#starting-context)
        * [More Layers](#more-layers)
        * [Modifying Elements](#modifying-elements)
    * [Naming Conventions in HTML](#naming-conventions-in-html)
    * [JavaScript Hooks](#javascript-hooks)
        * [`data-*` Attributes](#data--attributes)
    * [Taking It Further](#taking-it-further)
* [CSS Selectors](#css-selectors)
    * [Selector Intent](#selector-intent)
    * [Reusability](#reusability)
    * [Location Independence](#location-independence)
    * [Portability](#portability)
        * [Quasi-Qualified Selectors](#quasi-qualified-selectors)
    * [Naming](#naming)
        * [Naming UI Components](#naming-ui-components)
    * [Selector Performance](#selector-performance)
        * [The Key Selector](#the-key-selector)
    * [General Rules](#general-rules)

### Up Next

* Specificity
* Architecture
* Preprocessors
* Layout
* Performance
* Code Smells
* Legacy, Hacks, and Technical Debt

---

## Introduction

CSS is not a pretty language While it is simple to learn and get started with,
it soon becomes problematic at any reasonable scale. There isn’t much we can do
to change how CSS works, but we can make changes to the way we author and
structure it.

In working on large, long-running projects, with dozens of developers of
differing specialities and abilities, it is important that we all work in a
unified way in order to—among other things—

* keep stylesheets maintainable;
* keep code transparent, sane, and readable;
* keep stylesheets scalable.

There are a variety of techniques we must employ in order to satisfy these
goals, and <cite>CSS Guidelines</cite> is a document of recommendations and
approaches that will help us to do so.

### The Importance of a Styleguide

A coding styleguide (note, not a visual styleguide) is a valuable tool for teams
who

* build and maintain products for a reasonable length of time;
* have developers of differing abilities and specialisms;
* have a number of different developers working on a product at any given time;
* on-board new staff regularly;
* have a number of codebases that developers dip in and out of.

Whilst styleguides are typically more suited to product teams—large codebases on
long-lived and evolving projects, with multiple developers contributing over
prolonged periods of time—all developers should strive for a degree of
standardisation in their code.

A good styleguide, when well followed, will

* set the standard for code quality across a codebase;
* promote consistency across codebases;
* give developers a feeling of familiarity across codebases;
* increase productivity.

Styleguides should be learned, understood, and implemented at all times on a
project which is governed by one, and any deviation must be fully justified.

### Disclaimers

<cite>CSS Guidelines</cite> is _a_ styleguide; it is not _the_ styleguide. It
contains methodologies, techniques, and tips that I would firmly recommend to my
clients and teams, but your own tastes and circumstances may well be different.
Your mileage may vary.

These guidelines are opinionated, but they have been repeatedly tried, tested,
stressed, refined, broken, reworked, and revisited over a number of years on
projects of all sizes.

---

## Syntax and Formatting

One of the simplest forms of a styleguide is a set of rules regarding syntax and
formatting. Having a standard way of writing (_literally_ writing) CSS means
that code will always look and feel familiar to all members of the team.

Further, code that looks clean _feels_ clean. It is a much nicer environment to
work in, and prompts other team members to maintain the standard of cleanliness
that they found. Ugly code sets a bad precedent.

At a very high-level, we want

* Four (4) space indents. No tabs;
* 80 character wide columns;
* Multi-line CSS;
* Meaningful use of whitespace.

But, as with anything, the specifics are somewhat irrelevant—consistency is key.

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

* the ability to have multiple files open side by side;
* viewing CSS on sites like GitHub, or in terminal windows;
* providing a comfortable line length for comments.

<pre><code>/**
 * I am a long-form comment. I describe, in detail, the CSS that follows. I am
 * such a long comment that I easily break the 80 character limit, so I am
 * broken across several lines.
 */</code></pre>

There will be unavoidable exceptions to this rule—such as URLs, or gradient
syntax—which shouldn’t be worried about.

### Titling

Begin every new major section of a CSS project with a title:

    /*------------------------------------*\
        #SECTION-TITLE
    \*------------------------------------*/

    .selector {}

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

    .selector {}





    /*------------------------------------*\
        #ANOTHER-SECTION
    \*------------------------------------*/

    /**
     * Comment
     */

    .another-selector {}

{% include promo-buy.html %}

### Anatomy of a Ruleset

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

* related selectors on the same line; unrelated selectors on new lines;
* a space before our opening brace (`{`);
* properties and values on the same line;
* a space after our property–value delimiting colon (`:`);
* each declaration on its own new line;
* the opening brace (`{`) on the same line as our last selector;
* our first declaration on a new line after our opening brace (`{`);
* our closing brace (`}`) on its own new line;
* each declaration indented by four (4) spaces;
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

* tabs instead of spaces;
* unrelated selectors on the same line;
* the opening brace (`{`) on its own line;
* the closing brace (`}`) does not sit on its own line;
* the trailing (and, admittedly, optional) semi-colon (`;`) is missing;
* no spaces after colons (`:`).

### Multi-line CSS

CSS should be written across multiple lines, except in very specific
circumstances. There are a number of benefits to this:

* A reduced chance of merge conflicts, because each piece of functionality
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

* they still conform to the one-reason-to-change-per-line rule;
* they share enough similarities that they don’t need to be read as thoroughly
  as other rulesets—there is more benefit in being able to scan their selectors,
  which are of more interest to us in these cases.

### Indenting

As well as intending individual declarations, indent entire related rulesets to
signal their relation to one another, for example:

    .foo {}

        .foo__bar {}

            .foo__baz {}

By doing this, a developer can see at a glance that `.foo__baz {}` lives inside
`.foo__bar {}` lives inside `.foo {}`.

This quasi-replication of the DOM tells developers a lot about where classes are
expected to be used without them having to refer to a snippet of HTML.

#### Indenting Sass

Sass provides nesting functionality. That is to say, by writing this:

    .foo {
        color: red;

        .bar {
            color: blue;
        }

    }

…we will be left with this compiled CSS:

    .foo { color: red; }
    .foo .bar { color: blue; }

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

    .foo {}

        .foo__bar {}


    .foo--baz {}





    /*------------------------------------*\
        #BAR
    \*------------------------------------*/

    .bar {}

        .bar__baz {}

        .bar__foo {}

There should never be a scenario in which two rulesets do not have an empty line
between them. This would be incorrect:

    .foo {}
        .foo__bar {}
    .foo--baz {}

### HTML

Given HTML and CSS’ inherently interconnected nature, it would be remiss of me
to not cover some syntax and formatting guidelines for markup.

Always quote attributes, even if they would work without. This reduces the
chance of accidents, and is a more familiar format to the majority of
developers. For all this would work (and is valid):

    <div class=box>

…this format is preferred:

    <div class="box">

The quotes are not required here, but err on the safe side and include them.

When writing multiple values in a class attribute, separate them with two
spaces, thus:

    <div class="foo  bar">

When multiple classes are related to each other, consider grouping them in
square brackets (`[` and `]`), like so:

    <div class="[ box  box--highlight ]  [ bio  bio--long ]">

This is not a firm recommendation, and is something I am still trialling myself,
but it does carry a number of benefits. Read more in [<cite>Grouping related
classes in your
markup</cite>](http://csswizardry.com/2014/05/grouping-related-classes-in-your-markup/).

As with our rulesets, it is possible to use meaningful whitespace in your HTML.
You can denote thematic breaks in content with five (5) empty lines, for
example:

    <header class="page-head">
        ...
    </header>





    <main class="page-content">
        ...
    </main>





    <footer class="page-foot">
        ...
    </footer>

{% include promo-hire.html %}

Separate independent but loosely related snippets of markup with a single empty
line, for example:

    <ul class="primary-nav">

        <li class="primary-nav__item">
            <a href="/" class="primary-nav__link">Home</a>
        </li>

        <li class="primary-nav__item  primary-nav__trigger">
            <a href="/about" class="primary-nav__link">About</a>

            <ul class="primary-nav__sub-nav">
                <li><a href="/about/products">Products</a></li>
                <li><a href="/about/company">Company</a></li>
            </ul>

        </li>

        <li class="primary-nav__item">
            <a href="/contact" class="primary-nav__link">Contact</a>
        </li>

    </ul>

This allows developers to spot separate parts of the DOM at a glance, and also
allows certain text editors—like Vim, for example—to manipulate
empty-line-delimited blocks of markup.

### Further Reading

* [<cite>Grouping related classes in your markup</cite>](http://csswizardry.com/2014/05/grouping-related-classes-in-your-markup/)

---

## Commenting

The cognitive overhead of working with CSS is huge. With so much to be aware of,
and so many project-specific nuances to remember, the worst situation most
developers find themselves in is being the-person-who-didn’t-write-this-code.
Remembering your own classes, rules, objects, and helpers is manageable _to an
extent_, but anyone inheriting CSS barely stands a chance.

**CSS needs more comments.**

As CSS is something of a declarative language that doesn’t really leave much of
a paper-trail, it is often hard to discern—from looking at the CSS alone—

* whether some CSS relies on other code elsewhere;
* what effect changing some code will have elsewhere;
* where else some CSS might be used;
* what styles something might inherit (intentionally or otherwise);
* what styles something might pass on (intentionally or otherwise);
* where the author intended a piece of CSS to be used.

This doesn’t even take into account some of CSS’ many quirks—such as various
sates of `overflow` triggering block formatting context, or certain transform
properties triggering hardware acceleration—that make it even more baffling to
developers inheriting projects.

As a result of CSS not telling its own story very well, it is a language that
really does benefit from being heavily commented.

As a rule, you should comment anything that isn’t immediately obvious from the
code alone. That is to say, there is no need to tell someone that `color: red;`
will make something red, but if you’re using `overflow: hidden;` to clear
floats—as opposed to clipping an element’s overflow—this is probably something
worth documenting.

### High-level

For large comments that document entire sections or components, we use a
DocBlock-esque multi-line comment which adheres to our 80 column width.

Here is a real-life example from the CSS which styles the page header on [CSS
Wizardry](http://csswizardry.com/):

    /**
     * The site’s main page-head can have two different states:
     *
     * 1) Regular page-head with no backgrounds or extra treatments; it just
     *    contains the logo and nav.
     * 2) A masthead that has a fluid-height (becoming fixed after a certain point)
     *    which has a large background image, and some supporting text.
     *
     * The regular page-head is incredibly simple, but the masthead version has some
     * slightly intermingled dependency with the wrapper that lives inside it.
     */

This level of detail should be the norm for all non-trivial code—descriptions of
states, permutations, conditions, and treatments.

#### Object–Extension Pointers

When working across multiple partials, or in an OOCSS manner, you will often
find that rulesets that can work in conjunction with each other are not always
in the same file or location. For example, you may have a generic button
object—which provides purely structural styles—which is to be extended in a
component-level partial which will add cosmetics. We document this relationship
across files with simple <i>object–extension pointers</i>. In the object file:

    /**
     * Extend `.btn {}` in _components.buttons.scss.
     */

    .btn {}

And in your theme file:

    /**
     * These rules extend `.btn {}` in _objects.buttons.scss.
     */

    .btn--positive {}

    .btn--negative {}

This simple, low effort commenting can make a lot of difference to developers
who are unaware of relationships across projects, or who are wanting to know
how, why, and where other styles might be being inherited from.

### Low-level

Oftentimes we want to comment on specific declarations (i.e. lines) in a
ruleset. To do this we use a kind of reverse footnote. Here is a more complex
comment detailing the larger site headers mentioned above:

    /**
     * Large site headers act more like mastheads. They have a faux-fluid-height
     * which is controlled by the wrapping element inside it.
     *
     * 1. Mastheads will typically have dark backgrounds, so we need to make sure
     *    the contrast is okay. This value is subject to change as the background
     *    image changes.
     * 2. We need to delegate a lot of the masthead’s layout to its wrapper element
     *    rather than the masthead itself: it is to this wrapper that most things
     *    are positioned.
     * 3. The wrapper needs positioning context for us to lay our nav and masthead
     *    text in.
     * 4. Faux-fluid-height technique: simply create the illusion of fluid height by
     *    creating space via a percentage padding, and then position everything over
     *    the top of that. This percentage gives us a 16:9 ratio.
     * 5. When the viewport is at 758px wide, our 16:9 ratio means that the masthead
     *    is currently rendered at 480px high. Let’s…
     * 6. …seamlessly snip off the fluid feature at this height, and…
     * 7. …fix the height at 480px. This means that we should see no jumps in height
     *    as the masthead moves from fluid to fixed. This actual value takes into
     *    account the padding and the top border on the header itself.
     */

    .page-head--masthead {
        margin-bottom: 0;
        background: url(/img/css/masthead.jpg) center center #2e2620;
        @include vendor(background-size, cover);
        color: $color-masthead; /* [1] */
        border-top-color: $color-masthead;
        border-bottom-width: 0;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1) inset;

        @include media-query(lap-and-up) {
            background-image: url(/img/css/masthead-medium.jpg);
        }

        @include media-query(desk) {
            background-image: url(/img/css/masthead-large.jpg);
        }

        > .wrapper { /* [2] */
            position: relative; /* [3] */
            padding-top: 56.25%; /* [4] */

            @media screen and (min-width: 758px) { /* [5] */
                padding-top: 0; /* [6] */
                height: $header-max-height - double($spacing-unit) - $header-border-width; /* [7] */
            }

        }

    }

These types of comment allow us to keep all of our documentation in one place
whilst referring to the parts of the ruleset to which they belong.

### Preprocessor Comments

With most—if not all—preprocessors, we have the option to write comments that
will not get compiled out into our resulting CSS file. As a rule, use these
comments to document code that would not get written out to that CSS file
either. If you are documenting code which will get compiled, use comments that
will compile also. For example, this is correct:

    // Dimensions of the @2x image sprite:
    $sprite-width:  920px;
    $sprite-height: 212px;
    
    /**
     * 1. Default icon size is 16px.
     * 2. Squash down the retina sprite to display at the correct size.
     */
    .sprite {
        width:  16px; /* [1] */
        height: 16px; /* [1] */
        background-image: url(/img/sprites/main.png);
        background-size: ($sprite-width / 2 ) ($sprite-height / 2); /* [2] */
    }

We have documented variables—code which will not get compiled into our CSS
file—with preprocessor comments, whereas our CSS—code which will get compiled
into our CSS file—is documented using CSS comments. This means that we have only
the correct and relevant information available to us when debugging our compiled
stylesheets.

### Removing Comments

It should go without saying that no comments should make their way into
production environments—all CSS should be minified, resulting in loss of
comments, before being deployed.

---

## Naming Conventions

Naming conventions in CSS are hugely useful in making your code more
strict, more transparent, and more informative.

A good naming convention will tell you and your team

* what type of thing a class does;
* where a class can be used;
* what (else) a class might be related to.

The naming convention I follow is very simple: hyphen (`-`) delimited strings,
with BEM-like naming for more complex pieces of code.

It’s worth noting that a naming convention is not normally useful CSS-side of
development; they really come into their own when viewed in HTML.

### Hyphen Delimited

All strings in classes are delimited with a hyphen (`-`), like so:

    .page-head {}

    .sub-content {}

Camel case and underscores are not used for regular classes; the following are
incorrect:

    .pageHead {}

    .sub_content {}

{% include promo-buy.html %}

### BEM-like Naming

For larger, more interrelated pieces of UI that require a number of classes, we
use a BEM-like naming convention.

<cite>BEM</cite>, meaning <i>Block</i>, <i>Element</i>, <i>Modifier</i>, is a
front-end methodology coined by developers working at Yandex. Whilst BEM is a
complete methodology, here we are only concerned with its naming convention.
Further, the naming convention here only is BEM-*like*; the principles are
exactly the same, but the actual syntax differs slightly.

BEM splits components’ classes into three groups:

* Block: The sole root of the component.
* Element: A component part of the Block.
* Modifier: A variant or extension of the Block.

To take an analogy (note, not an example):

    .person {}
    .person__head {}
    .person--tall {}

Elements are delimited with two (2) underscores (`__`), and Modifiers are
delimited by two (2) hyphens (`--`).

Here we can see that `.person {}` is the Block; it is the sole root of a
discrete entity. `.person__head {}` is an Element; it is a smaller part of the
`.person {}` Block. Finally, `.person--tall {}` is a Modifier; it is a specific
variant of the `.person {}` Block.

#### Starting Context

Your Block context starts at the most logical, self-contained, discrete
location. To continue with our person-based analogy, we’d not have a class like
`.room__person {}`, as the room is another, much higher context. We’d probably
have separate Blocks, like so:

    .room {}

        .room__door {}

    .room--kitchen {}


    .person {}

        .person__head {}

If we did want to denote a `.person {}` inside a `.room {}`, it is more correct
to use a selector like `.room .person {}` which bridges two Blocks than it is to
increase the scope of existing Blocks and Elements.

A more realistic example of properly scoped blocks might look something like
this, where each chunk of code represents its own Block:

    .page {}


    .content {}


    .sub-content {}


    .footer {}

        .footer__copyright {}

Incorrect notation for this would be:

    .page {}

        .page__content {}

        .page__sub-content {}

        .page__footer {}

            .page__copyright {}

It is important to know when BEM scope starts and stops. As a rule, BEM applies
to self-contained, discrete parts of the UI.

#### More Layers

If we were to add another Element—called, let’s say, `.person__eye {}`—to this
`.person {}` component, we would not need to step through every layer of the
DOM. That is to say, the correct notation would be `.person__eye {}`, and not
`.person__head__eye {}`. Your classes do not reflect the full paper-trail of the
DOM.

#### Modifying Elements

You can have variants of Elements, and these can be denoted in a number of ways
depending on how and why they are being modified. Carrying on with our person
example, a blue eye might look like this:

    .person__eye--blue {}

Here we can see we’re directly modifying the eye Element.

Things can get more complex, however. Please excuse the crude analogy, and let’s
imagine we have a face Element that is handsome. The person themselves isn’t
that handsome, so we modify the face Element directly—a handsome face on a
regular person:

    .person__face--handsome {}

But what if that person _is_ handsome, and we want to style their face because
of that fact? A regular face on a handsome person:

    .person--handsome .person__face {}

Here is one of a few occasions where we’d use a descendant selector to modify
an Element based on a Modifier on the Block.

If using Sass, we would likely write this like so:

    .person {}

        .person__face {

            .person--handsome & {}

        }

    .person--handsome {}

Note that we do not nest a new instance of `.person__face {}` inside of
`.person--handsome {}`; instead, we make use of Sass’ parent selectors to
prepend `.person--handsome` onto the existing `.person__face {}` selector. This
means that all of our `.person__face {}`-related rules exist in once place, and
aren’t spread throughout the file. This is general good practice when dealing
with nested code: keep all of your context (e.g. all `.person__face {}` code)
encapsulated in one location.

### Naming Conventions in HTML

As I previously hinted at, naming conventions aren’t necessarily all that useful
in your CSS. Where naming conventions’ power really lies is in your markup. Take
the following, non-naming-conventioned HTML:

    <div class="box  profile  pro-user">

        <img class="avatar  image" />

        <p class="bio">...</p>

    </div>

How are the classes `box` and `profile` related to each other? How are the
classes `profile` and `avatar` related to each other? Are they related at all?
Should you be using `pro-user` alongside `bio`? Will the classes `image` and
`profile` live in the same part of the CSS? Can you use `avatar` anywhere else?

From that markup alone, it is very hard to answer any of those questions. Using
a naming convention, however, changes all that:

    <div class="box  profile  profile--is-pro-user">

        <img class="avatar  profile__image" />

        <p class="profile__bio">...</p>

    </div>

Now we can clearly see which classes are and are not related to each other, and
how; we know what classes we can’t use outside of the scope of this component;
and we know which classes we may be free to reuse elsewhere.

### JavaScript Hooks

As a rule, it is unwise to bind your CSS and your JS onto the same class in your
HTML. This is because doing so means you can’t have (or remove) one without
(removing) the other. It is much cleaner, much more transparent, and much more
maintainable to bind your JS onto specific classes.

I have known occasions before when trying to refactor some CSS has unwittingly
removed JS functionality because the two were tied to each other—it was
impossible to have one without the other.

Typically, these are classes that are prepended with `js-`, for example:

    <input type="submit" class="btn  js-btn" Value='Follow" />

This means that we can have an element elsewhere which can carry with style of
`.btn {}`, but without the behaviour of `.js-btn`.

#### `data-*` Attributes

A common practice is to use `data-*` attributes as JS hooks, but this is
incorrect. `data-*` attributes, as per the spec, are used <q>**to store custom
data** private to the page or application</q> (emphasis mine). `data-*`
attributes are designed to store data, not be bound to.

### Taking It Further

As previously mentioned, these are very simple naming conventions, and ones that
don’t do much more than denote three distinct groups of class.

I would encourage you to read up on and further look in to your naming
convention in order to provide more functionality—I know it’s something I’m keen
to research and investigate further.

### Further Reading

* [<cite>MindBEMding – getting your head ’round BEM syntax</cite>](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)

---

## CSS Selectors

Perhaps somewhat surprisingly, one of the most fundamental, critical aspects of
writing maintainable and scalable CSS is selectors. Their specificity, their
portability, and their reusability all have a direct impact on the mileage we
will get out of our CSS, and the headaches it might bring us.

### Selector Intent

It is important when writing CSS that we scope our selectors correctly, and that
we’re selecting the right things for the right reasons. <i>Selector Intent</i>
is the process of deciding and defining what you want to style and how you
will go about selecting it. For example, if you are wanting to style your
website’s main navigation menu, a selector like this would be incredibly unwise:

    header ul {}

This selector’s intent is to style any `ul` inside any `header` element, whereas
_our_ intent was to style the site’s main navigation. This is poor Selector
Intent: you can have any number of `header` elements on a page, and they in turn
can house any number of `ul`s, so a selector like this runs the risk of applying
very specific styling to a very wide number of elements. This will result in
having to write more CSS to undo the greedy nature of such a selector.

A better approach would be a selector like:

    .site-nav {}

An unambiguous, explicit selector with good Selector Intent. We are explicitly
selecting the right thing for exactly the right reason.

Poor Selector Intent is one of the biggest reasons for headaches on CSS
projects. Writing rules that are far too greedy—and that apply very specific
treatments via very far reaching selectors—causes unexpected side effects and
leads to very tangled stylesheets, with selectors overstepping their intentions
and impacting and interfering with otherwise unrelated rulesets.

CSS cannot be encapsulated, it is inherently leaky, but we can mitigate some of
these effects by not writing such globally-operating selectors: **your selectors
should be as explicit and well reasoned as your reason for wanting to select
something.**

### Reusability

With a move toward a more component-based approach to constructing UIs, the idea
of reusability is paramount. We want the option to be able to move, recycle,
duplicate, and syndicate components across our projects.

To this end, we make heavy use of classes. IDs, as well as being hugely
over-specific, cannot be used more than once on any given page, whereas classes
can be reused an infinite amount of times. Everything you choose, from the type
of selector to its name, should lend itself toward being reused.

### Location Independence

Given the ever-changing nature of most UI projects, and the move to more
component-based architectures, it is in our interests not to style things based
on where they are, but on _what_ they are. That is to say, our components’
styling should not be reliant upon where we place them—they should remain
entirely location independent.

Let’s take an example of a call-to-action button that we have chosen to style
via the following selector:

    .promo a {}

Not only does this have poor Selector Intent—it will greedily style any and
every link inside of a `.promo` to look like a button—it is also pretty wasteful
as a result of being so locationally dependent: we can’t reuse that button with
its correct styling outside of `.promo` because it is explicitly tied to that
location. A far better selector would have been:

    .btn {}

This single class can be reused anywhere outside of `.promo` and will always
carry its correct styling. As a result of a better selector, this piece of UI is
more portable, more recyclable, doesn’t have any dependencies, and has much
better Selector Intent. **A component shouldn’t have to live in a certain place
to look a certain way.**

{% include promo-hire.html %}

### Portability

Reducing, or, ideally, removing, location dependence means that we can move
components around our markup more freely, but how about improving our ability to
move classes around components? On a much lower level, there are changes we
can make to our selectors that make the selectors themselves—as opposed to the
components they create—more portable. Take the following example:

    input.btn {}

This is a <i>qualified</i> selector; the leading `input` ties this ruleset to
only being able to work on `input` elements. By omitting this qualification, we
allow ourselves to reuse the `.btn` class on any element we choose, like an `a`,
for example, or a `button`.

Qualified selectors do not lend themselves well to being reused, and every
selector we write should be authored with reuse in mind.

Of course, there are times when you may want to legitimately qualify a
selector—you might need to apply some very specific styling to a particular
element when it carries a certain class, for example:

    /**
     * Embolden and colour any element with a class of `.error`.
     */
    .error {
        color: red;
        font-weight: bold;
    }

    /**
     * If the element is a `div`, also give it some box-like styling.
     */
    div.error {
        padding: 10px;
        border: 1px solid;
    }

This is one example where a qualified selector might be justifiable, but I would
still recommend an approach more like:

    /**
     * Text-level errors.
     */
    .error-text {
        color: red;
        font-weight: bold;
    }

    /**
     * Elements that contain errors.
     */
    .error-box {
        padding: 10px;
        border: 1px solid;
    }

This means that we can apply `.error-box` to any element, and not just a
`div`—it is more reusable than a qualified selector.

#### Quasi-Qualified Selectors

One thing that qualified selectors can be useful for is signalling where a class
might be expected or intended to be used, for example:

    ul.nav {}

Here we can see that the `.nav` class is meant to be used on a `ul` element, and
not on a `nav`. By using <i>quasi-qualified selectors</i> we can still provide
that information without actually qualifying the selector:

    /*ul*/.nav {}

By commenting out the leading element, we can still leave it to be read, but
avoid qualifying and increasing the specificity of the selector.

### Naming

As Phil Karlton once said, <q>There are only two hard things in Computer
Science: cache invalidation and naming things.</q>

I won’t comment on the former claim here, but the latter has plagued me for
years.  My advice with regard to naming things in CSS is to pick a name that is
sensible, but somewhat ambiguous: aim for high reusability. For example, instead
of a class like `.site-nav`, choose something like `.primary-nav`; rather than
`.footer-links`, favour a class like `.sub-links`.

The differences in these names is that the first of each two examples is tied to
a very specific use case: they can only be used as the site’s navigation or the
footer’s links respectively. By using slightly more ambiguous names, we can
increase our ability to reuse these components in different circumstances.

To quote Nicolas Gallagher: <q>Tying your class name semantics tightly to the
nature of the content has already reduced the ability of your architecture to
scale or be easily put to use by other developers.</q>

That is to say, we should use sensible names—classes like `.border` or `.red`
are never advisable—but we should avoid using classes which describe the exact
nature of the content and/or its use cases. **Using a class name to describe
content is redundant because content describes itself.**

The debate surrounding semantics has raged for years, but it is important that
we adopt a more pragmatic, sensible approach to naming things in order to work
more efficiently and effectively. Instead of focussing on ‘semantics’, look more
closely at sensibility and longevity—choose names based on ease of maintenance,
not for their perceived meaning.

Name things for people; they’re the only things that actually _read_ your
classes (everything else merely matches them). Once again, it is better to
strive for reusable, recyclable classes rather than writing for specific use
cases. Let’s take an example:

    /**
     * Runs the risk of becoming out of date; not very maintainable.
     */
    .blue {
        color: blue;
    }

    /**
     * Depends on location in order to be rendered properly.
     */
    .header span {
        color: blue;
    }

    /**
     * Too specific; limits our ability to reuse.
     */
    .header-color {
        color: blue;
    }

    /**
     * Nicely abstracted, very portable, doesn’t risk becoming out of date.
     */
    .highlight-color {
        color: blue;
    }

It is important to strike a balance between names that do not literally describe
the style that the class brings, but also ones that do not explicitly describe
specific use cases. Instead of `.home-page-panel`, choose `.masthead`; instead
of `.site-nav`, favour `.primary-nav`; instead of `.btn-login`, opt for
`.btn-primary`.

#### Naming UI Components

Naming components with agnosticism and reusability in mind really helps
developers construct and modify UIs much more quickly, and with far less waste.
However, it can sometimes be beneficial to provide more specific or meaningful
naming alongside the more ambiguous class, particularly when several agnostic
classes come together to form a more complex and specific component that might
benefit from having a more meaningful name. In this scenario, we augment the
classes with a  `data-ui-component` attribute which houses a more specific name,
for example:

    <ul class="tabbed-nav" data-ui-component="Main Nav">

Here we have the benefits of a highly reusable class name which does not
describe—and, therefore, tie itself to—a specific use case, and added meaning
via our `data-ui-component` attribute. The `data-ui-component`’s value can take
any format you wish, like title case:

    <ul class="tabbed-nav" data-ui-component="Main Nav">

Or class-like:

    <ul class="tabbed-nav" data-ui-component="main-nav">

Or namespaced:

    <ul class="tabbed-nav" data-ui-component="nav-main">

The implementation is largely personal preference, but the concept still
remains: **Add any useful or specific meaning via a mechanism that will not
inhibit your and your team’s ability to recycle and reuse CSS.**

### Selector Performance

A topic which is—with the quality of today’s browsers—more interesting than it
is important, is selector performance. That is to say, how quickly a browser can
match the selectors your write in CSS up with the nodes it finds in the DOM.

Generally speaking, the longer a selector is (i.e. the more component parts) the
slower it is, for example:

    body.home div.header ul {}

…is a far less efficient selector than:

    .primary-nav {}

This is because browsers read CSS selectors **right-to-left**. A browser will
read the first selector as

* find all `ul` elements in the DOM;
* now check if they live anywhere inside an element with a class of `.header`;
* next check that `.header` class exists on a `div` element;
* now check that that all lives anywhere inside any elements with a class of
  `.home`;
* finally, check that `.home` exists on a `body` element.

The second, in contrast, is simply a case of the browser reading

* find all the elements with a class of `.primary-nav`.

To further compound the problem, we are using descendant selectors (e.g. `.foo
.bar {}`). The upshot of this is that a browser is required to start with the
rightmost part of the selector (i.e. `.bar`) and keep looking up the DOM
indefinitely until it finds the next part (i.e. `.foo`). This could mean
stepping up the DOM dozens of times until a match is found.

This is just one reason why **nesting with preprocessors is often a false
economy**; as well as making selectors unnecessarily more specific, and creating
location dependency, it also creates more work for the browser.

By using a child selector (e.g. `.foo > .bar {}`) we can make the process much
more efficient, because this only requires the browser to look one level higher
in the DOM, and it will stop regardless of whether or not it found a match.

#### The Key Selector

Because browsers read selectors right-to-left, the rightmost selector is often
critical in defining a selector’s performance: this is called the <i>key
selector</i>.

The following selector might appear to be highly performant at first glance. It
uses an ID which is nice and fast, and there can only ever be one on a page, so
surely this will be a nice and speedy lookup—just find that one ID and then
style everything inside of it:

    #foo * {}

The problem with this selector is that the key selector (`*`) is very, _very_
far reaching. What this selector actually does is finds _every single_ node in
the DOM (even `<title>`, `<link>`, and `<head>` elements; _everything_) and then
looks to see if it lives anywhere at any level within `#foo`. This is a very,
_very_ expensive selector, and should most likely be avoided or rewritten.

Thankfully, by writing selectors with good [Selector Intent](#selector-intent),
we are probably avoiding inefficient selectors by default; we are very unlikely
to have greedy key selectors if we’re targeting the right things for the right
reason.

That said, however, CSS selector performance should be fairly low on your list
of things to optimise; browsers are fast, and are only ever getting faster, and
it is only on notable edge cases that inefficient selectors would be likely to
pose a problem.

As well as their own specific issues, nesting, qualifying, and poor Selector
Intent all contribute to less efficient selectors.

### General Rules

Your selectors are fundamental to writing good CSS. To very briefly sum up the
above sections:

* **Select what you want explicitly**, rather than relying on circumstance or
  coincidence. Good Selector Intent will rein in the reach and leak of your
  styles.
* **Write selectors for reusability**, so that you can work more efficiently and
  reduce waste and repetition.
* **Do not nest selectors unnecessarily**, because this will increase
  specificity and affect where else you can use your styles.
* **Do not qualify selectors unnecessarily**, as this will impact the number of
  different elements you can apply styles to.
* **Keep selectors as short as possible**, in order to keep specificity down and
  performance up.

Focussing on these points will keep your selectors a lot more sane and easy to
work with on changing and long-running projects.

### Further Reading

* [<cite>Shoot to kill; CSS selector intent</cite>](http://csswizardry.com/2012/07/shoot-to-kill-css-selector-intent/)
* [<cite>‘Scope’ in CSS</cite>](http://csswizardry.com/2013/05/scope-in-css/)
* [<cite>Keep your CSS selectors short</cite>](http://csswizardry.com/2012/05/keep-your-css-selectors-short/)
* [<cite>About HTML semantics and front-end architecture</cite>](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/)
* [<cite>Naming UI components in OOCSS</cite>](http://csswizardry.com/2014/03/naming-ui-components-in-oocss/)
* [<cite>Writing efficient CSS selectors</cite>](http://csswizardry.com/2011/09/writing-efficient-css-selectors/)

---
