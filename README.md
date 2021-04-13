# gotoAndPlay CSS Style Guide

Based on Harry Roberts' [CSS Guidelines](https://github.com/csswizardry/CSS-Guidelines).

*High-level advice and guidelines for writing sane, manageable, scalable CSS*

## Introduction

  CSS is not a pretty language. While it is simple to learn and get started with, it soon becomes problematic at any reasonable scale. There isn’t much we can do to change how CSS works, but we can make changes to the way we author and structure it.

  In working on large, long-running projects, with dozens of developers of differing specialities and abilities, it is important that we all work in a unified way in order to—among other things—

  * keep stylesheets maintainable;
  * keep code transparent, sane, and readable;
  * keep stylesheets scalable.

  There are a variety of techniques we must employ in order to satisfy these goals, and CSS Guidelines is a document of recommendations and approaches that will help us to do so.

## The Importance of Styleguide

  A coding styleguide (note, not a visual styleguide) is a valuable tool for teams who

  * build and maintain products for a reasonable length of time;
  * have developers of differing abilities and specialisms;
  * have a number of different developers working on a product at any given time;
  * on-board new staff regularly;
  * have a number of codebases that developers dip in and out of.

  Whilst styleguides are typically more suited to product teams—large codebases on long-lived and evolving projects, with multiple developers contributing over prolonged periods of time—all developers should strive for a degree of standardisation in their code.

  A good styleguide, when well followed, will

  * set the standard for code quality across a codebase;
  * promote consistency across codebases;
  * give developers a feeling of familiarity across codebases;
  * increase productivity.

  Styleguides should be learned, understood, and implemented at all times on a project which is governed by one, and any deviation must be fully justified.

## Disclaimers

  These guidelines are opinionated, but they have been repeatedly tried, tested, stressed, refined, broken, reworked, and revisited over a number of years on projects of all sizes.

## Syntax and Formatting

  One of the simplest forms of a styleguide is a set of rules regarding syntax and formatting. Having a standard way of writing (literally writing) CSS means that code will always look and feel familiar to all members of the team.

  Further, code that looks clean feels clean. It is a much nicer environment to work in, and prompts other team members to maintain the standard of cleanliness that they found. Ugly code sets a bad precedent.

  At a very high-level, we want

  * four (4) space indents, no tabs; [stylelint/indentation](https://stylelint.io/user-guide/rules/indentation)
  * multi-line CSS;
  * meaningful use of whitespace.

  But, as with anything, the specifics are somewhat irrelevant — consistency is key.

### Multiple Files

  Split discrete chunks of code into their own files, which are concatenated during a build step.

  We encourage splitting each components' styles to a separate file.

### 80 Characters Wide Comments

  [stylelint/max-line-length](https://stylelint.io/user-guide/rules/max-line-length)

  ```css
    /**
    * I am a long-form comment. I describe, in detail, the CSS that follows. I am
    * such a long comment that I easily break the 80 character limit, so I am
    * broken across several lines.
    */
  ```

  This rule should be applied only to comments, exempting all CSS declarations.

## Anatomy of a Ruleset

  Before we discuss how we write out our rulesets, let’s first familiarise ourselves with the relevant terminology:

  ```css
  [selector] {
      [property]: [value];
      [<--declaration--->]
  }
  ```

  For example:

  ```css
  .foo,
  .foo--bar,
  .baz {
      display: block;
      background-color: green;
      color: red;
  }
  ```

  Here you can see we have

  * each selector on its own new line;
  * a space before our opening brace ( <a>{</a> );
  * properties and values on the same line;
  * a space after our property–value delimiting colon ( <a>:</a> ); [stylelint/declaration-colon-space-after](https://stylelint.io/user-guide/rules/declaration-colon-space-after)
  * each declaration on its own new line; [stylelint/declaration-block-semicolon-newline-after](https://stylelint.io/user-guide/rules/declaration-block-semicolon-newline-after)
  * the opening brace ( <a>{</a> ) on the same line as our last selector;
  * our first declaration on a new line after our opening brace ( <a>{</a> ); [stylelint/block-opening-brace-newline-after](https://stylelint.io/user-guide/rules/block-opening-brace-newline-after)
  * our closing brace ( <a>}</a> ) on its own new line;
  * each declaration indented by four (4) spaces; [stylelint/indentation](https://stylelint.io/user-guide/rules/indentation)
  * a trailing semi-colon ( <a>;</a> ) on our last declaration. [stylelint/declaration-block-trailing-semicolon](https://stylelint.io/user-guide/rules/declaration-block-trailing-semicolon)

  As such, the following would be incorrect:

  ```css
    .foo, .foo--bar, .baz
    {
      display:block;
      background-color:green;
      color:red }
  ```

  Problems here include

  * tabs instead of spaces;
  * unrelated selectors on the same line;
  * the opening brace ( <a>{</a> ) on its own line;
  * the closing brace ( <a>}</a> ) does not sit on its own line;
  * the trailing (and, admittedly, optional) semi-colon ( <a>;</a> ) is missing;
  * no spaces after colons ( <a>:</a> ).

### Multi-line CSS

  CSS should be written across multiple lines. There are a number of benefits to this:

  * A reduced chance of merge conflicts, because each piece of functionality exists on its own line.
  * More ‘truthful’ and reliable <a>diffs</a>, because one line only ever carries one change.

  For example:

  ```css
  .icon {
      display: inline-block;
      width:  16px;
      height: 16px;
      background-image: url(/img/sprite.svg);
  }
  ```

### Indenting

  Do not indent same level declaration blocks differently:

```scss
.foo { }

.foo__bar { }

// indent nested Sass rulesets the same way, with four (4) spaces
.foo__baz {
    .foo--top & {}
}
```

## Meaningful Whitespace

  As well as indentation, we can provide a lot of information through conservative and judicious use of whitespace between rulesets. We use one (1) empty line between rulesets.

  For example:

  ```css
  .foo { }

  .foo__bar { }

  .foo--baz { }

  .bar { }

  .bar__baz { }

  .bar__foo { }
  ```

  There should never be a scenario in which two rulesets do not have an empty line between them. This would be incorrect:

  ```css
    .foo { }
    .foo__bar { }
    .foo--baz { }
  ```

## Commenting

  The cognitive overhead of working with CSS is huge. With so much to be aware of, and so many project-specific nuances to remember, the worst situation most developers find themselves in is being the-person-who-didn’t-write-this-code. Remembering your own classes, rules, objects, and helpers is manageable to an extent, but anyone inheriting CSS barely stands a chance.

  <b>CSS needs more comments.</b>

  As CSS is something of a declarative language that doesn’t really leave much of a paper-trail, it is often hard to discern—from looking at the CSS alone—

  * whether some CSS relies on other code elsewhere;
  * what effect changing some code will have elsewhere;
  * where else some CSS might be used;
  * what styles something might inherit (intentionally or otherwise);
  * what styles something might pass on (intentionally or otherwise);
  * where the author intended a piece of CSS to be used.

  This doesn’t even take into account some of CSS’ many quirks—such as various sates of <a>overflow</a> triggering block formatting context, or certain transform properties triggering hardware acceleration—that make it even more baffling to developers inheriting projects.

  As a result of CSS not telling its own story very well, it is a language that really does benefit from being heavily commented.

  As a rule, you should comment anything that isn’t immediately obvious from the code alone. That is to say, there is no need to tell someone that <a>color: red;</a> will make something red, but if you’re using <a>overflow: hidden;</a> to clear floats—as opposed to clipping an element’s overflow—this is probably something worth documenting.

### Multi-line vs single-line

  If your comment spans multiple lines, use DocBlock-esque multi-line comments. In other cases, use single-line comments.

  ```scss
  // single-line-comment

  /**
   * Multi-line comment
   *
   * 1) Regular page-head with no backgrounds or extra treatments; it just
   *    contains the logo and nav.
   * 2) A masthead that has a fluid-height (becoming fixed after a certain point)
   *    which has a large background image, and some supporting text.
   *
   * The regular page-head is incredibly simple, but the masthead version has some
   * slightly intermingled dependency with the wrapper that lives inside it.
   */
  ```

  This level of detail should be the norm for all non-trivial code—descriptions of states, permutations, conditions, and treatments.

### Low-level

  Oftentimes we want to comment on specific declarations (i.e. lines) in a ruleset. Add these comments directly before the declarations.

  ```scss
  .header__inner {
      display: flex;
      align-items: center;
      justify-content: space-between;

      @media only screen and (max-width: $bp-md-min - 1) {
          position: fixed;
          z-index: 1;
          top: 0;
          left: 0;
          right: 0;
          bottom: 0;
          overflow: auto;
          // background color is always related to text color
          background-color: $color-text-03;
          flex-wrap: wrap;
          align-items: flex-start;
          padding-top: $header-height;
          opacity: 0;
          visibility: hidden;
          transition: $transition-duration $transition-easing;
          transition-property: opacity, visibility;
      }
  }
  ```

  These types of comments allow us to keep all of our documentation together with the ruleset to which they belong. This splits up the documentation into smaller chunks that are easier to reason about and understand.

### Removing Comments

  It should go without saying that no comments should make their way into production environments—all CSS should be minified, resulting in loss of comments, before being deployed.

## Naming Conventions

  Naming conventions in CSS are hugely useful in making your code more strict, more transparent, and more informative.

  A good naming convention will tell you and your team

  * what type of thing a class does;
  * where a class can be used;
  * what (else) a class might be related to.

  The naming convention we follow is very simple: hyphen (-) delimited strings, with [BEM](http://getbem.com/)-like naming for more complex pieces of code.

  It’s worth noting that a naming convention is not normally useful CSS-side of development; they really come into their own when viewed in HTML.

### Hyphen Delimited

  All strings in classes are delimited with a hyphen (-), like so:

  ```css
    .page-head { }

    .sub-content { }
  ```

  Camel case and underscores are not used for regular classes; the following are incorrect:

  ```css
    .pageHead { }

    .sub_content { }
  ```

### BEM-like Naming

  For larger, more interrelated pieces of UI that require a number of classes, we use a BEM-like naming convention.

  BEM, meaning <i>Block</i>, <i>Element</i>, <i>Modifier</i>, is a front-end methodology coined by developers working at Yandex. Whilst BEM is a complete methodology, here we are only concerned with its naming convention. Further, the naming convention here only is BEM-like; the principles are exactly the same, but the actual syntax differs slightly.

  To take an analogy (note, not an example):

  ```css
    .person { }
    .person--tall { }
    .person__head { }
  ```

  Elements are delimited with two (2) underscores (__), and Modifiers are delimited by two (2) hyphens (--).

  Here we can see that <a>.person {}</a> is the Block; it is the sole root of a discrete entity. <a>.person__head {}</a> is an Element; it is a smaller part of the <a>.person {}</a> Block. Finally, <a>.person--tall {}</a> is a Modifier; it is a specific variant of the <a>.person {}</a> Block.

## Starting Context

  Your Block context starts at the most logical, self-contained, discrete location. To continue with our person-based analogy, we’d not have a class like <a>.room__person {}</a>, as the room is another, much higher context. We’d probably have separate Blocks, like so:

  ```css
    .room { }

    .room--kitchen { }

    .room__door { }

    .person { }

    .person__head { }
  ```

  If we did want to denote a <a>.person {}</a> inside a <a>.room {}</a>, it is more correct to use a selector like <a>.room__human {}</a> which bridges two Blocks than it is to increase the scope of existing Blocks and Elements. Keep in mind when "adopting" a child as parent's element, the element name does not have to correspond to the adopted block, rather it's element name should be relevant in the context.

  A more realistic example of properly scoped blocks might look something like this, where each chunk of code represents its own Block:

  ```css
    .page { }

    .content { }

    .sub-content { }

    .footer { }

    .footer__copyright { }
  ```

  Incorrect notation for this would be:

  ```css
    .page { }

    .page__content { }

    .page__sub-content { }

    .page__footer { }

    .page__copyright { }
  ```

  It is important to know when BEM scope starts and stops. As a rule, BEM applies to self-contained, discrete parts of the UI.

### More Layers

  If we were to add another Element—called, let’s say, <a>.person__eye {}</a>—to this <a>.person {}</a> component, we would not need to step through every layer of the DOM. That is to say, the correct notation would be <a>.person__eye {}</a>, and not <a>.person__head__eye {}</a>. Your classes do not reflect the full paper-trail of the DOM.

### Modifying Elements

  You can have variants of Elements, and these can be denoted in a number of ways depending on how and why they are being modified. Carrying on with our person example, a blue eye might look like this:

  ```css
    .person__eye--blue { }
  ```

  Here we can see we’re directly modifying the eye Element.

  Things can get more complex, however. Please excuse the crude analogy, and let’s imagine we have a face Element that is handsome. The person themselves isn’t that handsome, so we modify the face Element directly—a handsome face on a regular person:

  ```css
    .person__face--handsome { }
  ```

  But what if that person is handsome, and we want to style their face because of that fact? A regular face on a handsome person:

  ```css
    .person--handsome .person__face { }
  ```

  Here is one of a few occasions where we’d use a descendant selector to modify an Element based on a Modifier on the Block.

  If using Sass, we would likely write this like so:

  ```scss
    .person { }

    .person--handsome { }

    .person__face {
        .person--handsome & { }
    }
  ```

  Note that we do not nest a new instance of <a>.person__face {}</a> inside of <a>.person--handsome {}</a>; instead, we make use of Sass’ parent selectors to prepend <a>.person--handsome</a> onto the existing <a>.person__face {}</a> selector. This means that all of our <a>.person__face {}</a>-related rules exist in once place, and aren’t spread throughout the file. This is general good practice when dealing with nested code: keep all of your context (e.g. all <a>.person__face {}</a> code) encapsulated in one location.

### Naming Conventions in HTML

  As I previously hinted at, naming conventions aren’t necessarily all that useful in your CSS. Where naming conventions’ power really lies is in your markup. Take the following, non-naming-conventioned HTML:

  ```html
  <div class="box profile pro-user">

    <img class="avatar image" />

    <p class="bio">...</p>

  </div>
  ```

  How are the classes <a>box</a> and <a>profile</a> related to each other? How are the classes <a>profile</a> and <a>avatar</a> related to each other? Are they related at all? Should you be using <a>pro-user</a> alongside bio? Will the classes <a>image</a> and <a>profile</a> live in the same part of the CSS? Can you use <a>avatar</a> anywhere else?

  From that markup alone, it is very hard to answer any of those questions. Using a naming convention, however, changes all that:

  ```html
    <div class="box profile profile--is-pro-user">

      <img class="avatar profile__image" />

      <p class="profile__bio">...</p>

    </div>
  ```

  Now we can clearly see which classes are and are not related to each other, and how; we know what classes we can’t use outside of the scope of this component; and we know which classes we may be free to reuse elsewhere.

### JavaScript Hooks

  As a general rule, hook your JS to the same class used for styling. This is because your styles, HTML and JS functionality are very tightly coupled.

  If the JS functionality is optional, however, it is recommended to use an optional class that is prefixed with `js-`, for example:

  ```html
    <a href="#next-section" class="btn js-scroll-to">Scroll to next section</a>
  ```

  This means that we can have an element elsewhere which can carry with style of `.btn {}`, but without the behaviour of `.js-scroll-to`.

  #### <b>data-</b> Attributes

  A common practice is to use <a>data-*</a> attributes as JS hooks, but this is incorrect. <a>data-*</a> attributes, as per the spec, are used <b>to store custom data</b> private to the page or application (emphasis mine). <a>data-*</a> attributes are designed to store data, not be bound to.

  Third party plugins are exempt from this rule.

### Taking It Further

  As previously mentioned, these are very simple naming conventions, and ones that don’t do much more than denote three distinct groups of class.

  I would encourage you to read up on and further look in to your naming convention in order to provide more functionality—I know it’s something I’m keen to research and investigate further.

## CSS Selectors

  Perhaps somewhat surprisingly, one of the most fundamental, critical aspects of writing maintainable and scalable CSS is selectors. Their specificity, their portability, and their reusability all have a direct impact on the mileage we will get out of our CSS, and the headaches it might bring us.

### Selector Intent

  It is important when writing CSS that we scope our selectors correctly, and that we’re selecting the right things for the right reasons. Selector Intent is the process of deciding and defining what you want to style and how you will go about selecting it. For example, if you are wanting to style your website’s main navigation menu, a selector like this would be incredibly unwise:

  ```css
    header ul { }
  ```

  This selector’s intent is to style any <a>ul</a> inside any <a>header</a> element, whereas our intent was to style the site’s main navigation. This is poor Selector Intent: you can have any number of header <a>elements</a> on a page, and they in turn can house any number of <a>ul</a>s, so a selector like this runs the risk of applying very specific styling to a very wide number of elements. This will result in having to write more CSS to undo the greedy nature of such a selector.

  A better approach would be a selector like:

  ```css
    .site-nav { }
  ```

  An unambiguous, explicit selector with good Selector Intent. We are explicitly selecting the right thing for exactly the right reason.

  Poor Selector Intent is one of the biggest reasons for headaches on CSS projects. Writing rules that are far too greedy—and that apply very specific treatments via very far reaching selectors—causes unexpected side effects and leads to very tangled stylesheets, with selectors overstepping their intentions and impacting and interfering with otherwise unrelated rulesets.

  CSS cannot be encapsulated, it is inherently leaky, but we can mitigate some of these effects by not writing such globally-operating selectors: <b>your selectors should be as explicit and well reasoned as your reason for wanting to select something.</b>

### Reusability

  With a move toward a more component-based approach to constructing UIs, the idea of reusability is paramount. We want the option to be able to move, recycle, duplicate, and syndicate components across our projects.

  To this end, we make heavy use of classes. IDs, as well as being hugely over-specific, cannot be used more than once on any given page, whereas classes can be reused an infinite amount of times. Everything you choose, from the type of selector to its name, should lend itself toward being reused.

### Location Independence

  Given the ever-changing nature of most UI projects, and the move to more component-based architectures, it is in our interests not to style things based on where they are, but on what they are. That is to say, our components’ styling should not be reliant upon where we place them—they should remain entirely location independent.

  Let’s take an example of a call-to-action button that we have chosen to style via the following selector:

  ```css
    .promo a { }
  ```

  Not only does this have poor Selector Intent—it will greedily style any and every link inside of a <a>.promo</a> to look like a button—it is also pretty wasteful as a result of being so locationally dependent: we can’t reuse that button with its correct styling outside of .promo because it is explicitly tied to that location. A far better selector would have been:

  ```css
    .btn { }
  ```

  This single class can be reused anywhere outside of <a>.promo</a> and will always carry its correct styling. As a result of a better selector, this piece of UI is more portable, more recyclable, doesn’t have any dependencies, and has much better Selector Intent. <b>A component shouldn’t have to live in a certain place to look a certain way.</b>

### Portability

  Reducing, or, ideally, removing, location dependence means that we can move components around our markup more freely, but how about improving our ability to move classes around components? On a much lower level, there are changes we can make to our selectors that make the selectors themselves—as opposed to the components they create—more portable. Take the following example:

```css
    input.btn { }
```

  This is a qualified selector; the leading <a>input</a> ties this ruleset to only being able to work on <a>input</a> elements. By omitting this qualification, we allow ourselves to reuse the <a>.btn</a> class on any element we choose, like an <a>a</a>, for example, or a <a>button</a>.

  Qualified selectors do not lend themselves well to being reused, and every selector we write should be authored with reuse in mind.

  Of course, there are times when you may want to legitimately qualify a selector—you might need to apply some very specific styling to a particular element when it carries a certain class, for example:


```scss
// Embolden and colour any element with a class of `.card`.
.card {
    color: red;
    font-weight: bold;
}

// If the element is a `a`, also give it some hover styling.
a.card {
    &:hover {
        transform: translateY(-6px);
    }
}
```

  This is one example where a qualified selector might be justifiable, but I would still recommend an approach more like:

```scss
.card {
    color: red;
    font-weight: bold;
}

.card--link {
    &:hover {
        transform: translateY(-6px);
    }
}
```

  This means that we can apply `.card--link` to any element, and not just an a—it is more reusable than a qualified selector.

### Naming

  As Phil Karlton once said,
  > There are only two hard things in Computer Science: cache invalidation and naming things.

  We won’t comment on the former claim here, but the latter has plagued me for years. Our advice with regard to naming things in CSS is to pick a name that is sensible, but somewhat ambiguous: aim for high reusability. For example, instead of a class like <a>.site-nav</a>, choose something like <a>.primary-nav</a>; rather than <a>.footer-links</a>, favour a class like <a>.sub-links</a>.

  The differences in these names is that the first of each two examples is tied to a very specific use case: they can only be used as the site’s navigation or the footer’s links respectively. By using slightly more ambiguous names, we can increase our ability to reuse these components in different circumstances.

  To quote Nicolas Gallagher:

  > Tying your class name semantics tightly to the nature of the content has already reduced the ability of your architecture to scale or be easily put to use by other developers.

  That is to say, we should use sensible names—classes like <a>.border</a> or <a>.red</a> are never advisable—but we should avoid using classes which describe the exact nature of the content and/or its use cases. <b>Using a class name to describe content is redundant because content describes itself.</b>

  The debate surrounding semantics has raged for years, but it is important that we adopt a more pragmatic, sensible approach to naming things in order to work more efficiently and effectively. Instead of focussing on ‘semantics’, look more closely at sensibility and longevity—choose names based on ease of maintenance, not for their perceived meaning.

  Name things for people; they’re the only things that actually read your classes (everything else merely matches them). Once again, it is better to strive for reusable, recyclable classes rather than writing for specific use cases. Let’s take an example:

  ```css
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
  ```

  It is important to strike a balance between names that do not literally describe the style that the class brings, but also ones that do not explicitly describe specific use cases. Instead of <a>.home-page-panel</a>, choose <a>.hero</a>; instead of <a>.site-nav</a>, favour <a>.primary-nav</a>; instead of <a>.btn-login</a>, opt for <a>.btn-primary</a>.

### General Rules

  Your selectors are fundamental to writing good CSS. To very briefly sum up the above sections:

  * <b>Select what you want explicitly</b>, rather than relying on circumstance or coincidence. Good Selector Intent will rein in the reach and leak of your styles.
  * <b>Write selectors for reusability</b>, so that you can work more efficiently and reduce waste and repetition.
  * <b>Do not nest selectors unnecessarily</b>, because this will increase specificity and affect where else you can use your styles.
  * <b>Do not qualify selectors unnecessarily</b>, as this will impact the number of different elements you can apply styles to.
  * <b>Keep selectors as short as possible</b>, in order to keep specificity down and performance up.

  Focussing on these points will keep your selectors a lot more sane and easy to work with on changing and long-running projects.

### Specificity

  As we’ve seen, CSS isn’t the most friendly of languages: globally operating, very leaky, dependent on location, hard to encapsulate, based on inheritance… But! None of that even comes close to the horrors of specificity.

  No matter how well considered your naming, regardless of how perfect your source order and cascade are managed, and how well you’ve scoped your rulesets, just one overly-specific selector can undo everything. It is a gigantic curveball, and undermines CSS’ very nature of the cascade, inheritance, and source order.

  The problem with specificity is that it sets precedents and trumps that cannot simply be undone. If we take a real example that I was responsible for some years ago:

  ```css
    #content table { }
  ```

  Not only does this exhibit poor <a><b>Selector Intent</b></a>—I didn’t actually want every table in the <a>#content</a> area, I wanted a specific type of <a>table</a> that just happened to live there—it is a hugely over-specific selector. This became apparent a number of weeks later, when I needed a second type of <a>table</a>:

  ```css
    #content table { }

    /**
     * Uh oh! My styles get overwritten by `#content table {}`.
     */
    .my-new-table { }
  ```

  The first selector was trumping the specificity of the one defined after it, working against CSS’ source-order based application of styles. In order to remedy this, I had two main options. I could

  1. refactor my CSS and HTML to remove that ID;
  1. write a more specific selector to override it.

  Unfortunately, refactoring would have taken a long time; it was a mature product and the knock-on effects of removing this ID would have been a more substantial business cost than the second option: just write a more specific selector.

  ```css
    #content table { }

    #content .my-new-table { }
  ```

  Now I have a selector that is even more specific still! And if I ever want to override this one, I will need another selector of at least the same specificity defined after it. I’ve started on a downward spiral.

  Specificity can, among other things,

  * limit your ability to extend and manipulate a codebase;
  * interrupt and undo CSS’ cascading, inheriting nature;
  * cause avoidable verbosity in your project;
  * prevent things from working as expected when moved into different environments;
  * lead to serious developer frustration.

  All of these issues are greatly magnified when working on a larger project with a number of developers contributing code.

#### Keep It Low at All Times

  The problem with specificity isn’t necessarily that it’s high or low; it’s the fact it is so variant and that it cannot be opted out of: the only way to deal with it is to get progressively more specific—the notorious specificity wars we looked at above.

  One of the single, simplest tips for an easier life when writing CSS—particularly at any reasonable scale—is to keep always try and keep specificity as low as possible at all times. Try to make sure there isn’t a lot of variance between selectors in your codebase, and that all selectors strive for as low a specificity as possible.

  Doing so will instantly help you tame and manage your project, meaning that no overly-specific selectors are likely to impact or affect anything of a lower specificity elsewhere. It also means you’re less likely to need to fight your way out of specificity corners, and you’ll probably also be writing much smaller stylesheets.

  Simple changes to the way we work include, but are not limited to,

  * not using IDs in your CSS;
  * not nesting selectors;
  * not qualifying classes;
  * not chaining selectors.

  <b>Specificity can be wrangled and understood, but it is safer just to avoid it entirely.</b>

#### IDs in CSS

  If we want to keep specificity low, which we do, we have one really quick-win, simple, easy-to-follow rule that we can employ to help us: avoid using IDs in CSS.

  Not only are IDs inherently non-reusable, they are also vastly more specific than any other selector, and therefore become specificity anomalies. Where the rest of your selectors are relatively low specificity, your ID-based selectors are, comparatively, much, <i>much</i> higher.

  In fact, to highlight the severity of this difference, see how <i>one thousand</i> chained classes cannot override the specificity of a single ID: <a href="jsfiddle.net/0yb7rque">jsfiddle.net/0yb7rque</a>. (Please note that in Firefox you may see the text rendering in blue: this is a <a href="https://twitter.com/codepo8/status/505004085398224896">known bug</a>, and an ID will be overridden by 256 chained classes.)

  <b>N.B</b>. It is still perfectly okay to use IDs in HTML and JavaScript; it is only in CSS that they prove troublesome.

  It is often suggested that developers who choose not to use IDs in CSS merely don’t understand how specificity works. This is as incorrect as it is offensive: no matter how experienced a developer you are, this behaviour cannot be circumvented; no amount of knowledge will make an ID less specific.

  Opting into this way of working only introduces the chance of problems occurring further down the line, and—particularly when working at scale—all efforts should be made to avoid the potential for problems to arise. In a sentence:

  <b>It is just not worth introducing the risk.</b>

  As an exception, IDs can be used in CSS when there is a need to override a third party style that also uses IDs for styling.

### Nesting

  We’ve already looked at how nesting can lead to location dependent and potentially inefficient code, but now it’s time to take a look at another of its pitfalls: it makes selectors more specific.

  When we talk about nesting, we don’t necessarily mean preprocessor nesting, like so:

  ```scss
    .foo {

      .bar { }

    }
  ```

  We’re actually talking about descendant or child selectors; selectors which rely on a thing within a thing. That could look like any one of the following:

  ```scss
    /**
     * An element with a class of `.bar` anywhere inside an element with a class of
     * `.foo`.
     */
    .foo .bar { }


    /**
     * An element with a class of `.module-title` directly inside an element with a
     * class of `.module`.
     */
    .module > .module-title { }


    /**
     * Any `li` element anywhere inside a `ul` element anywhere inside a `nav`
     * element
     */
    nav ul li { }
  ```

  Whether you arrive at this CSS via a preprocessor or not isn’t particularly important, but it is worth noting that <b>preprocessors tout this as a feature, where is actually to be avoided wherever possible.</b>

  Generally speaking, each part in a compound selector adds specificity. Ergo, the fewer parts to a compound selector then the lower its overall specificity, and we always want to keep specificity low. To quote Jonathan Snook:

  > …whenever declaring your styles, use the least number of selectors required to style an element.

  Let’s look at an example:

  ```css
    .widget {
        padding: 10px;
    }

    .widget > .widget__title {
        color: red;
    }
  ```

  To style an element with a class of <a>.widget__title</a>, we have a selector that is twice as specific as it needs to be. That means that if we want to make any modifications to <a>.widget__title</a>, we’ll need another at-least-equally specific selector:

  ```css
    .widget { }

    .widget > .widget__title { }

    .widget > .widget__title--sub {
        color: blue;
    }
  ```

  Not only is this entirely avoidable—we caused this problem ourselves—we have a selector that is literally double the specificity it needs to be. We used 200% of the specificity actually required. And not only that, but this also leads to needless verbosity in our code—more to send over the wire.

  As a rule, <b>if a selector will work without it being nested then do not nest it</b>.

  Nesting and raising specificity is necessary when using state classes on a block (that need to override all possible modifiers) and when modifying an element based on block modifier.

```scss
    .widget {
        &.is-open { }
    }

    .widget__title {
        .widget--primary & { }
    }
```

## Scope

  One possible advantage of nesting—which, unfortunately, does not outweigh the disadvantages of increased specificity—is that it provides us with a namespace of sorts. A selector like <a>.widget</a> <a>.title</a> scopes the styling of <a>.title</a> to an element that only exists inside of an element carrying a class of <a>.widget</a>.

  This goes some way to providing our CSS with scope and encapsulation, but does still mean that our selectors are twice as specific as they need to be. A better way of providing this scope would be via a namespace—which we already have in the form of <a href="#bem-like-naming"><b>BEM-like Naming</b></a>—which does not lead to an unnecessary increase in specificity.

  Now we have better scoped CSS with minimal specificity—the best of both worlds.

## !important

  The word <a>!important</a> sends shivers down the spines of almost all front-end developers. <a>!important</a> is a direct manifestation of problems with specificity; it is a way of cheating your way out of specificity wars, but usually comes at a heavy price. It is often viewed as a last resort—a desperate, defeated stab at patching over the symptoms of a much bigger problem with your code.

  The general rule is that <a>!important</a> is always a bad thing, but, to quote Jamie Mason:

  > Rules are the children of principles.

  That is to say, a single rule is a simple, black-and-white way of adhering to a much larger principle. When you’re starting out, the rule never use <a>!important</a> is a good one.

  However, once you begin to grow and mature as a developer, you begin to understand that the principle behind that rule is simply about keeping specificity low. You’ll also learn when and where the rules can be bent…

  <a>!important</a> does have a place in CSS projects, but only if used sparingly and proactively.

  Proactive use of <a>!important</a> is when it is used before you’ve encountered any specificity problems; when it is used as a guarantee rather than as a fix. For example:

  ```css
    .hidden {
        display: none !important;
    }
  ```

  This helper, or <i>utility</i>, class is very specific in their intentions: you would only use it if you wanted something to be not rendered at all. If you didn’t want this behaviour, you would not use this class, therefore whenever you do use it you will definitely want them to win.

  Here we proactively apply <a>!important</a> to ensure that these styles always win. This is correct use of <a>!important</a> to guarantee that these trumps always work, and don’t accidentally get overridden by something else more specific.

  Incorrect, reactive use of <a>!important</a> is when it is used to combat specificity problems after the fact: applying <a>!important</a> to declarations because of poorly architected CSS. For example, let’s imagine we have this HTML:

  ```html
    <div class="content">
      <h2 class="heading-sub">...</h2>
    </div>
  ```

  …and this CSS:

  ```css
    .content h2 {
      font-size: 2em;
    }

    .heading-sub {
      font-size: 1.5em !important;
    }
  ```

  Here we can see how we’ve used <a>!important</a> to force our <a>.heading-sub {}</a> styles to reactively override our <a>.content h2 {}</a> selector. This could have been circumvented by any number of things, including using better Selector Intent, or avoiding nesting.

  In these situations, it is preferable that you investigate and refactor any offending rulesets to try and bring specificity down across the board, as opposed to introducing such specificity heavyweights.

  <b>Only use <a>!important</a> proactively, not reactively.</b>

  As an exception, `!important` can be used reactively when there is a need to override a third party styles that are too specific.

## Hacking Specificity

  With all that said on the topic of specificity, and keeping it low, it is inevitable that we will encounter problems. No matter how hard we try, and how conscientious we are, there will always be times that we need to hack and wrangle specificity.

  When these situations do arise, it is important that we handle the hacks as safely and elegantly as possible.

  In the event that you need to increase the specificity of a class selector, there are a number of options. We could nest the class inside something else to bring its specificity up. For example, we could use <a>.header .site-nav {}</a> to bring up the specificity of a simple <a>.site-nav {}</a> selector.

  The problem with this, as we’ve discussed, is that it introduces location dependency: these styles will only work when the <a>.site-nav</a> component is in the <a>.header</a> component.

  Instead, we can use a much safer hack that will not impact this component’s portability: we can chain that class with itself:

  ```css
    .site-nav.site-nav { }
  ```

  This chaining doubles the specificity of the selector, but does not introduce any dependency on location.

  In the event that we do, for whatever reason, have an ID in our markup that we cannot replace with a class, select it via an attribute selector as opposed to an ID selector. For example, let’s imagine we have embedded a third-party widget on our page. We can style the widget via the markup that it outputs, but we have no ability to edit that markup ourselves:

  ```html
    <div id="third-party-widget">
      ...
    </div>
  ```

  Even though we know not to use IDs in CSS, what other option do we have? We want to style this HTML but have no access to it, and all it has on it is an ID.

  We do this:

  ```css
    [id="third-party-widget"] { }
  ```

  Here we are selecting based on an attribute rather than an ID, and attribute selectors have the same specificity as a class. This allows us to style based on an ID, but without introducing its specificity.

  Do keep in mind that these are hacks, and should not be used unless you have no better alternative.

## Architectural Principles

  You would be forgiven for thinking that an architecture for CSS is a somewhat grandiose and unnecessary concept: why would something so simple, so straightforward, need something as complex or considered as an architecture?!

  Well, as we’ve seen, CSS’ simplicity, its looseness, and its unruly nature mean that the best way of managing (read, taming) it at any reasonable scale is through a strict and specific architecture. A solid architecture can help us control our specificity, enforce naming conventions, manage our source order, create a sane development environment, and generally make managing our CSS projects a lot more consistent and comfortable.

  There is no tool, no preprocessor, no magic bullet, that will make your CSS better on its own: a developer’s best tool when working with such a loose syntax is self-discipline, conscientiousness, and diligence, and a well-defined architecture will help enforce and facilitate these traits.

  Architectures are large, overarching, principle-led collections of smaller conventions which come together to provide a managed environment in which code is written and maintained. Architectures are typically quite high level, and leave implementation details—such as naming conventions or syntax and formatting, for example—to the team implementing it.

  Most architectures are usually based around existing design patterns and paradigms, and, more often than not, these paradigms were born of computer scientists and software engineers. For all CSS isn’t ‘code’, and doesn’t exhibit many traits that programming languages do, we find that we can apply some of these same principles to our own work.

  In this section, we’ll take a look at some of these design patterns and paradigms, and how we can use them to reduce code—and increase code reuse—in our CSS projects.

### High-level Overview

  At a very high-level, your architecture should help you

  * provide a consistent and sane environment;
  * accommodate change;
  * grow and scale your codebase;
  * promote reuse and efficiency;
  * increase productivity.

  Typically, this will mean a class-based and componentised architecture, split up into manageable modules, probably using a preprocessor. Of course, there is far more to an architecture than that, so let’s look at some principles…

### Object-orientation

  Object-orientation is a programming paradigm that breaks larger programs up into smaller, in(ter)dependent objects that all have their own roles and responsibilities. From Wikipedia:

  > Object-oriented programming (OOP) is a programming paradigm that represents the concept of ‘objects’ […] which are usually instances of classes, [and] are used to interact with one another to design applications and computer programs.

  When applied to CSS, we call it object-oriented CSS, or OOCSS. OOCSS was coined and popularised by Nicole Sullivan, whose Media Object has become the poster child of the methodology.

  OOCSS deals with the separation of UIs into structure and skin: breaking UI components into their underlying structural forms, and layering their cosmetic forms on separately. This means that we can recycle common and recurring design patterns very cheaply without having to necessarily recycle their specific implementation details at the same time. OOCSS promotes reuse of code, which makes us quicker, as well as keeping the size of our codebase down.

  Structural aspects can be thought of like skeletons; common, recurring frames that provide design-free constructs known as objects and abstractions. Objects and abstractions are simple design patterns that are devoid of any cosmetics; we abstract out the shared structural traits from a series of components into a generic object.

  Skin is a layer that we (optionally) add to our structure in order to give objects and abstractions a specific look-and-feel. Let’s look at an example:

  ```css
    /**
     * A simple, design-free alert object. Extend this object with a `.alert--*` skin
     * class.
     */
    .alert {
        display: flex;
        align-items: flex-start;
        padding: 12px 16px;
    }

    /**
     * Success alerts skin. Extends `.alert`.
     */
    .alert--success {
        background-color: green;
    }

    /**
     * Error alerts' skin. Extends `.alert`.
     */
    .alert--error {
        background-color: red;
    }
  ```

  Above, we can see how the <a>.alert {}</a> class simply provides structural styling to an element, and doesn’t concern itself with any cosmetics. We supplement the <a>.alert {}</a> object with a second class, such as <a>.alert--negative {}</a> in order to give that DOM node specific cosmetics:

  ```html
    <div class="alert alert--success">Success!</div>
  ```

  Favour the multiple-class approach over using something like <a>@extend</a>: using multiple classes in your markup—as opposed to wrapping the classes up into one using a preprocessor—

  * gives you a better paper-trail in your markup, and allows you to see quickly and explicitly which classes are acting on a piece of HTML;
  * allows for greater composition in that classes are not tightly bound to other styles in your CSS.

  Whenever you are building a UI component, try and see if you can break it into two parts: one for structural styles (paddings, layout, etc.) and another for skin (colours, typefaces, etc.).

### The Single Responsibility Principle

  The single responsibility principle is a paradigm that, very loosely, states that all pieces of code (in our case, classes) should focus on doing one thing and one thing only. More formally:

  > …the single responsibility principle states that every context (class, function, variable, etc.) should have a single responsibility, and that responsibility should be entirely encapsulated by the context.

  What this means for us is that our CSS should be composed of a series of much smaller classes that focus on providing very specific and limited functionality. This means that we need to decompose UIs into their smallest component pieces that each serve a single responsibility; they all do just one job, but can be very easily combined and composed to make much more versatile and complex constructs. Let’s take some example CSS that does not adhere to the single responsibility principle:

  ```css
    .error-message {
      display: block;
      padding: 10px;
      border-top: 1px solid #f00;
      border-bottom: 1px solid #f00;
      background-color: #fee;
      color: #f00;
      font-weight: bold;
      text-align: right;
    }

    .success-message {
      display: block;
      padding: 10px;
      border-top: 1px solid #0f0;
      border-bottom: 1px solid #0f0;
      background-color: #efe;
      color: #0f0;
      font-weight: bold;
      text-align: center;
    }
  ```

  Here we can see that—despite being named after one very specific use-case—these classes are handling quite a lot: layout, structure, and cosmetics. We also have a lot of repetition. We need to refactor this in order to abstract out some shared objects (OOCSS) and bring it more inline with the single responsibility principle. We can break these two classes out into four much smaller responsibilities:

  ```css
    .message {
      border-style: solid;
      border-width: 1px 0;
      font-weight: bold;
    }

    /*
     * Theme variations
     */
    .message--color-error {
      background-color: #fee;
      color: #f00;
    }

    .message--color-success {
      background-color: #efe;
      color: #0f0;
    }

    /*
     * Alignment variations
     */
    .message--align-center {
        text-align: center;
    }

    .message--align-right {
        text-align: right;
    }
  ```

  Now we have a base message component that can be extended by a number of smaller responsibility classes. The amount of repetition has been greatly reduced, and our ability to extend and compose our CSS has been greatly increased. This is a great example of OOCSS and the single responsibility principle working in tandem.

  By focussing on single responsibilities, we can give our code much more flexibility, and extending components’ functions becomes very simple when sticking to the open/closed principle, which we’re going to look at next.

### The Open/Closed Principle

  The open/closed principle, in my opinion, is rather poorly named. It is poorly named because 50% of the vital information is omitted from its title. The open/closed principle states that

  > [s]oftware entities (classes, modules, functions, etc.) should be open for extension, but closed for modification.

  See? The most important words—extension and modification—are completely missing from the name, which isn’t very useful at all.

  Once you have trained yourself to remember what the words open and closed actually relate to, you’ll find that open/closed principle remarkably simple: any additions, new functionality, or features we add to our classes should be added via extension—we should not modify these classes directly. This really trains us to write bulletproof single responsibilities: because we shouldn’t modify objects and abstractions directly, we need to make sure we get them as simple as possible the first time. This means that we should never need to actually change an abstraction—we’d simply stop using it—but any slight variants of it can be made very easily by extending it.

  Let’s take an example:

  ```css
    .box {
      display: block;
      padding: 10px;
    }

    .box--large {
      padding: 20px;
    }
  ```

  Here we can see that the <a>.box {}</a> object is incredibly simple: we’ve stripped it right back into one very small and very focussed responsibility. To modify that box, we extend it with another class; <a>.box--large {}</a>. Here the <a>.box {}</a> class is closed to modification, but open to being extended.

  An incorrect way of achieving the same might look like this:

  ```css
  .box {
    display: block;
    padding: 10px;
  }

  .content .box {
    padding: 20px;
  }
  ```

  Not only is this overly specific, locationally dependent, and potentially displaying poor Selector Intent, we are modifying the <a>.box {}</a> directly. We should rarely—if ever—find an object or abstraction’s class as a key selector in a compound selector.

  A selector like <a>.content .box {}</a> is potentially troublesome because

  * it forces all <a>.box</a> components into that style when placed inside of <a>.content</a>, which means the modification is dictated to developers, whereas developers should be allowed to opt into changes explicitly;
  * the <a>.box</a> style is now unpredictable to developers; the single responsibility no longer exists because nesting the selector produces a forced caveat.

  All modifications, additions, and changes should always be opt-in, not mandatory. If you think something might need a slight adjustment to take it away from the norm, provide another class which adds this functionality.

  When working in a team environment, be sure to write API-like CSS; always ensure that existing classes remain backward compatible (i.e. no changes at their root) and provide new hooks to bring in new features. Changing the root object, abstraction, or component could have huge knock-on effects for developers making use of that code elsewhere, so never modify existing code directly.

  Exceptions may present themselves when it transpires that a root object does need a rewrite or refactor, but it is only in these specific cases that you should modify code. Remember: <b>open for extension; closed for modification.</b>

### DRY

  DRY, which stands for Don’t Repeat Repeat Yourself, is a micro-principle used in software development which aims to keep the repetition of key information to a minimum. Its formal definition is that

  > [E]very piece of knowledge must have a single, unambiguous, authoritative representation within a system.

  Although a very simple principle—in principle—DRY is often misinterpreted as the necessity to never repeat the exact same thing twice at all in a project. This is impractical and usually counterproductive, and can lead to forced abstractions, over-thought and -engineered code, and unusual dependencies.

  The key isn’t to avoid all repetition, but to normalise and abstract meaningful repetition. If two things happen to share the same declarations coincidentally, then we needn’t DRY anything out; that repetition is purely circumstantial and cannot be shared or abstracted. For example:

  ```css
    .btn {
      display: inline-block;
      padding: 1em 2em;
      font-weight: bold;
    }

    [...]

    .page-title {
      font-size: 3rem;
      line-height: 1.4;
      font-weight: bold;
    }

    [...]

      .user-profile__title {
        font-size: 1.2rem;
        line-height: 1.5;
        font-weight: bold;
      }
  ```

  From the above code, we can reasonably deduce that the <a>font-weight: bold</a>; declaration appears three times purely coincidentally. To try and create an abstraction, mixin, or <a>@extend</a> directive to cater for this repetition would be overkill, and would tie these three rulesets together based purely on circumstance.

  However, imagine we’re using a web-font that requires <a>font-weight: bold;</a> to be declared every time the <a>font-family</a> is:

  ```css
    .btn {
      display: inline-block;
      padding: 1em 2em;
      font-family: "My Web Font", sans-serif;
      font-weight: bold;
    }

    [...]

    .page-title {
      font-size: 3rem;
      line-height: 1.4;
      font-family: "My Web Font", sans-serif;
      font-weight: bold;
    }

    [...]

      .user-profile__title {
        font-size: 1.2rem;
        line-height: 1.5;
        font-family: "My Web Font", sans-serif;
        font-weight: bold;
      }
  ```

  Here we’re repeating a more meaningful snippet of CSS; these two declarations have to always be declared together. In this instance, we probably would DRY out our CSS.

  We would recommend using a mixin over <a>@extend</a> here because, even though the two declarations are thematically grouped, the rulesets themselves are still separate, unrelated entities: to use <a>@extend</a> would be to physically group these unrelated rulesets together in our CSS, thus making the unrelated related.

  Our mixin:

  ```scss
    @mixin my-web-font() {
      font-family: "My Web Font", sans-serif;
      font-weight: bold;
    }

    .btn {
      display: inline-block;
      padding: 1em 2em;
      @include my-web-font();
    }

    [...]

    .page-title {
      font-size: 3rem;
      line-height: 1.4;
      @include my-web-font();
    }

    [...]

      .user-profile__title {
        font-size: 1.2rem;
        line-height: 1.5;
        @include my-web-font();
      }
  ```

  Now the two declarations only exist once, meaning we’re not repeating ourselves. If we ever switch out our web-font, or move to a <a>font-weight: normal</a>; version, we only need to make that change in one place.

  In short, only DRY code that is actually, thematically related. Do not try to reduce purely coincidental repetition: <b>duplication is better than the wrong abstraction</b>.

### Composition over Inheritance

  Now that we’re used to spotting abstractions and creating single responsibilities, we should be in a great position to start composing more complex composites from a series of much smaller component parts. Nicole Sullivan likens this to using Lego; tiny, single responsibility pieces which can be combined in a number of different quantities and permutations to create a multitude of very different looking results.

  This idea of building through composition is not a new one, and is often referred to as composition over inheritance. This principle suggests that larger systems should be composed from much smaller, individual parts, rather than inheriting behaviour from a much larger, monolithic object. This should keep your code decoupled—nothing inherently relies on anything else.

  Composition is a very valuable principle for an architecture to make use of, particularly considering the move toward component-based UIs. It will mean you can more easily recycle and reuse functionality, as well rapidly construct larger parts of UI from a known set of composable objects. Think back to our error message example in the <b>[Single Responsibility Principle](#the-single-responsibility-principle)</b> section; we created a complete UI component by composing a number of much smaller and unrelated objects.

### The Separation of Concerns

  The separation of concerns is a principle which, at first, sounds a lot like the single responsibility principle. The separation of concerns states that code should be broken up

  > into distinct sections, such that each section addresses a separate concern. A concern is a set of information that affects the code of a computer program. […] A program that embodies SoC well is called a modular program.

  Modular is a word we’re probably used to; the idea of breaking UIs and CSS into much smaller, composable pieces. The separation of concerns is just a formal definition which covers the concepts of modularity and encapsulation in code. In CSS this means building individual components, and writing code which only focusses itself on one task at a time.

  The term was coined by Edsger W. Dijkstra, who rather elegantly said:

  > Let me try to explain to you, what to my taste is characteristic for all intelligent thinking. It is, that one is willing to study in depth an aspect of one’s subject matter in isolation for the sake of its own consistency, all the time knowing that one is occupying oneself only with one of the aspects. We know that a program must be correct and we can study it from that viewpoint only; we also know that it should be efficient and we can study its efficiency on another day, so to speak. In another mood we may ask ourselves whether, and if so: why, the program is desirable. But nothing is gained—on the contrary!—by tackling these various aspects simultaneously. It is what I sometimes have called ‘the separation of concerns’, which, even if not perfectly possible, is yet the only available technique for effective ordering of one’s thoughts, that I know of. This is what I mean by ‘focusing one’s attention upon some aspect’: it does not mean ignoring the other aspects, it is just doing justice to the fact that from this aspect’s point of view, the other is irrelevant. It is being one- and multiple-track minded simultaneously.

  Beautiful. The idea here is to focus fully on one thing at once; build one thing to do its job very well whilst paying as little attention as possible to other facets of your code. Once you have addressed and built all these separate concerns in isolation—meaning they’re probably very modular, decoupled, and encapsulated—you can begin bringing them together into a larger project, **which is a concern of it's own**.

  A great example is layout. If you are using a grid system, all of the code pertaining to layout should exist on its own, without including anything else. You’ve written code that handles layout, and that’s it:

  ```html
    <div class="layout">

      <div class="layout__item  two-thirds">
      </div>

      <div class="layout__item  one-third">
      </div>

    </div>
  ```

  You will now need to write new, separate code to handle what lives inside of that layout:

  ```html
    <div class="layout">

      <div class="layout__item  two-thirds">
        <section class="content">
          ...
        </section>
      </div>

      <div class="layout__item  one-third">
        <section class="sub-content">
          ...
        </section>
      </div>

    </div>
  ```

  The separation of concerns allows you to keep code self-sufficient, ignorant, and ultimately a lot more maintainable. Code which adheres to the separation of concerns can be much more confidently modified, edited, extended, and maintained because we know how far its responsibilities reach. We know that modifying layout, for example, will only ever modify layout—nothing else.

  The separation of concerns increases reusability and confidence whilst reducing dependency.

### Misconceptions

  There are a number of unfortunate misconceptions surrounding the separation of concerns when applied to HTML and CSS. They all seem to revolve around some format of:

  > Using classes for CSS in your markup breaks the separation of concerns.

  Unfortunately, this is simply not true. The separation of concerns <i>does</i> exist in the context of HTML and CSS (and JS), but not in the way a lot of people seem to believe.

  The separation of concerns when applied to front-end code is not about classes-in-HTML-purely-for-styling-hooks-blurring-the-lines-between-concerns; it is about the very fact that we are using different languages for markup and styling at all.

  Back before CSS was widely adopted, we’d use <a>table</a>s to lay content out, and <a>font</a> elements with <a>color</a> attributes to provide cosmetic styling. The problem here is that HTML was being used to create content and also to style it; there was no way of having one without the other. This was a complete lack of separation of concerns, which was a problem. CSS’ job was to provide a completely new syntax to apply this styling, allowing us to separate our content and style concerns across two technologies.

  Another common argument is that <i>putting classes in your HTML puts style information in your markup</i>.

  So, in a bid to circumvent this, people adopt selectors that might look a little like this:

```css
    body > header:first-of-type > nav > ul > li > a {
    }
```

  This CSS—presumably to style our site’s main nav—has the usual problems of location dependency, poor Selector Intent, and high specificity, but it also manages to do <i>exactly what developers are trying to avoid</i>, only in the opposite direction: <b>it puts DOM information in your CSS</b>. Aggressive attempts to avoid putting any style hints or hooks in markup only lead to overloading stylesheets with DOM information.

  In short: having classes in your markup does not violate the separation of concerns. Classes merely act as an API to link two separate concerns together. The simplest way to separate concerns is to write well formed HTML and well formed CSS, and link to two together with sensible, judicious use of classes.
