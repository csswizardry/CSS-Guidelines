# General CSS notes, advice and guidelines
# 普适性的 CSS 笔记、建议与指导

---

## Translations

* [Russian/русский](https://github.com/matmuchrapna/CSS-Guidelines/blob/master/README%20Russian.md)

---

In working on large, long running projects with dozens of developers, it is
important that we all work in a unified way in order to, among other things:
在参与规模庞大、历时漫长且人手众多的项目时，所有开发者遵守如下规则极为重要：

* Keep stylesheets maintainable
* Keep code transparent and readable
* Keep stylesheets scalable
* 保持 CSS 样式表的可维护性
* 保持代码清晰移动
* 保持代码的可拓展性

There are a variety of techniques we must employ in order to satisfy these
goals.
为了实现这一目标，我们应当使用诸多技术。

The first part of this document will deal with syntax, formatting and CSS
anatomy, the second part will deal with approach, mindframe and attitude toward
writing and architecting CSS. Exciting, huh?
本文档第一部分将探讨语法、格式以及 CSS 解析；第二部分将从方法论、思维框架、以及编写与规划 CSS 样式的态度入手。

## Contents 目录

* [CSS document anatomy](#css-document-anatomy)
  * [General](#general)
  * [One file vs. many files](#one-file-vs-many-files)
  * [Table of contents](#table-of-contents)
  * [Section titles](#section-titles)
* [Source order](#source-order)
* [Anatomy of rulesets](#anatomy-of-rulesets)
* [Naming conventions](#naming-conventions)
  * [JS hooks](#js-hooks)
  * [Internationalisation](#internationalisation)
* [Comments](#comments)
  * [Comments on steroids](#comments-on-steroids)
    * [Quasi-qualified selectors](#quasi-qualified-selectors)
    * [Tagging code](#tagging-code)
    * [Object/extension pointers](#objectextension-pointers)
* [Writing CSS](#writing-css)
* [Building new components](#building-new-components)
* [OOCSS](#oocss)
* [Layout](#layout)
* [Sizing UIs](#sizing-uis)
  * [Font sizing](#font-sizing)
* [Shorthand](#shorthand)
* [IDs](#ids)
* [Selectors](#selectors)
  * [Over qualified selectors](#over-qualified-selectors)
  * [Selector performance](#selector-performance)
* [CSS selector intent](#css-selector-intent)
* [`!important`](#important)
* [Magic numbers and absolutes](#magic-numbers-and-absolutes)
* [Conditional stylesheets](#conditional-stylesheets)
* [Debugging](#debugging)
* [Preprocessors](#preprocessors)

* [CSS 文档解析](#css-document-anatomy)
  * [总览](#general)
  * [单一文件与多文件](#one-file-vs-many-files)
  * [目录](#table-of-contents)
  * [章节标题](#section-titles)
* [代码顺序](#source-order)
* [规则解析](#anatomy-of-rulesets)
* [命名规范](#naming-conventions)
  * [JavaScript 钩子](#js-hooks)
  * [国际化](#internationalisation)
* [注释](#comments)
  * [更好的命名方式](#comments-on-steroids)
    * [Quasi-qualified selectors](#quasi-qualified-selectors)
    * [Tagging code](#tagging-code)
    * [Object/extension pointers](#objectextension-pointers)
* [编写 CSS](#writing-css)
* [添加新部分](#building-new-components)
* [面向对象 CSS](#oocss)
* [布局](#layout)
* [界面尺寸](#sizing-uis)
  * [字号调节](#font-sizing)
* [简写](#shorthand)
* [IDs](#ids)
* [选择器](#selectors)
  * [Over qualified selectors](#over-qualified-selectors)
  * [选择器性能](#selector-performance)
* [选择器继承](#css-selector-intent)
* [`!important`](#important)
* [魔法数字与绝对比例](#magic-numbers-and-absolutes)
* [带条件 CSS](#conditional-stylesheets)
* [Debugging](#debugging)
* [预处理](#preprocessors)

---

## CSS Document Anatomy CSS 文档解析

No matter the document, we must always try and keep a common formatting. This
means consistent commenting, consistent syntax and consistent naming.
无论文档如何，我们都应当尽力维持统一的风格，这包括统一的注释、统一的语法与统一的命名风格。

### General 总则

Limit your stylesheets to a maximum 80 character width where possible.
Exceptions may be gradient syntax and URLs in comments. That’s fine, there’s
nothing we can do about that.
尽量将行宽控制在 80 字符以下。除了渐变相关的语法以及注释中的 URL，毕竟这些我们本来也无法处理。

I prefer four (4) space indents over tabs and write multi-line CSS.
我倾向于用 4 个空格缩进、不用 Tab，并且将样式拆分成多行。

### One file vs. many files 单一文件与多文件

Some people prefer to work with single, large files. This is fine, and by
sticking to the following guidelines you’ll encounter no problems. Since moving
to Sass I have started sharding my stylesheets out into lots of tiny includes.
This too is fine… Whichever method you choose, the following rules and
guidelines apply. The only notable difference is with regards our table of
contents and our section titles. Read on for further explanation…
有些人喜欢将样式写成一个大文件，这并不赖，而且如果你遵守下文指导的话你也不会遇到什么问题。我在迁移至 Sass 之后，开始将样式拆分成众多小文件。这也不赖……无论你采用什么方式，下文中的规则都将适用。唯一的区别在于目录表以及区块标题。

### Table of contents 目录

At the top of stylesheets, I maintain a table of contents which will detail the
sections contained in the document, for example:
在样式表的开头，我会维护一份详解文档区块内容的目录，如下所示：

    /*------------------------------------*\
        $CONTENTS
    \*------------------------------------*/
    /**
     * CONTENTS............You’re reading it!
     * RESET...............Set our reset defaults
     * FONT-FACE...........Import brand font files
     */

This will tell the next developer(s) exactly what they can expect to find in
this file. Each item in the table of contents maps directly to a section title.  
这将告诉其它开发者这份文件中具体含有哪些内容。这份目录中的每一项都与其对应的区块标题相同。

If you are working in one big stylesheet, the corresponding section will also be
in that file. If you are working across multiple files then each item in the
table of contents will map to an include which pulls that section in.
如果你在维护一份大规模的样式表，对应的区块也将在这份文件中。如果你是在编写一群小文件，那么目录表中的每一项应当对应其相应的 @include 语句。

### Section titles 区块标题

The table of contents would be of no use unless it had corresponding section
titles. Denote a section thus:
如果目录表中没有对应区块标题的话，它就没有意义。注意如下的这个区块标题：

    /*------------------------------------*\
        $RESET
    \*------------------------------------*/

The `$` prefixing the name of the section allows us to run a find ([Cmd|Ctrl]+F)
for `$[SECTION-NAME]` and **limit our search scope to section titles only**.
在区块标题中前缀 `$` 可以让我们使用查找命令（[Cmd|Ctrl]+F）查找 `$[SECTION-NAME]` 并 **将查找范围仅仅限定在区块标题**。

If you are working in one large stylesheet, you leave five (5) carriage returns
between each section, thus:
如果你在维护一份大文件，那么在每个区块之间空 5 行，如下：

    /*------------------------------------*\
        $RESET
    \*------------------------------------*/
    [Our
    reset
    styles]
    
    
    
    
    
    /*------------------------------------*\
        $FONT-FACE
    \*------------------------------------*/

This large chunk of whitespace is quickly noticeable when scrolling quickly
through larger files.
在大文件中快速滚动时这些大块的空档非常显眼。

If you are working across multiple, included stylesheets, start each of those
files with a section title and there is no need for any carriage returns.
如果你在维护多份、以 include 连接的样式表的话，在每份文件头加上标题即可，可以不用这样空行。

## Source order 源文件顺序

Try and write stylesheets in specificity order. This ensures that you take full
advantage of inheritance and CSS’ first <i>C</i>; the cascade.
尽量按照特定顺序编写样式表，这样将确保你充分发挥 CSS 缩写中第一个 <i>C</i> 的意义：cascade，层叠。

A well ordered stylesheet will be ordered something like this:
一份规划良好的样式表应当按照如下排列：

1. **Reset** – ground zero.
2. **Elements** – unclassed `h1`, unclassed `ul` etc.
3. **Objects and abstractions** — generic, underlying design patterns.
4. **Components** – full components constructed from objects and their
   extensions.
5. **Style trumps** – error states etc.

1. **Reset** 万物之根源
2. **元素** 没有设置 clas 的 `h1`、`ul` 等
3. **对象以及抽象内容** 最一般、最基础的设计模式
4. **子元素** 从对象拓展出来的所有子元素及其子元素
5. **修补** 异常状态

This means that—as you go down the document—each section builds upon and
inherits sensibly from the previous one(s). There should be less undoing of
styles, less specificity problems and all-round better architected stylesheets.
这意味着你顺文档而下时，每个区块都将继承在它之前区块的属性。这样就可以减少代码相互抵消的部分，减少某些特殊的问题，构成设计更理想的样式表结构。

For further reading I cannot recommend Jonathan Snook’s
[SMACSS](http://smacss.com) highly enough.

关于这方面的更多信息，强烈推荐 Jonathan Snook 的 [SMACSS](http://smacss.com)。

## Anatomy of rulesets CSS 规则集解析

    [selector]{
        [property]:[value];
        [<- Declaration ->]
    }    

I have a number of standards when structuring rulesets.
编写规则集时，我有诸多标准。

* Use hyphen delimited class names (except for BEM notation,
  [see below](#naming-conventions))
* 4 space indented
* Multi-line
* Declarations in relevance (NOT alphabetical) order
* Indent vendor prefixed declarations so that their values are aligned
* Indent our rulesets to mirror the DOM
* Always include the final semi-colon in a ruleset

* class 名称以连字符（-）连接，除了[下文](#命名规范)中提到的 BEM 命名；
* 缩进 4 空格；
* 声明拆分成多行；
* 声明以相关性顺序排列，而非字母顺序；
* 有前缀的声明适当缩进，使得其值对齐；
* 缩进
* 保留最后一条声明结尾的分号

A brief example:
上例子：

    .widget{
        padding:10px;
        border:1px solid #BADA55;
        background-color:#C0FFEE;
        -webkit-border-radius:4px;
           -moz-border-radius:4px;
                border-radius:4px;
    }
        .widget-heading{
            font-size:1.5rem;
            line-height:1;
            font-weight:bold;
            color:#BADA55;
            margin-right:-10px;
            margin-left: -10px;
            padding:0.25em;
        }

Here we can see that `.widget-heading` must be a child of `.widget` as we have
indented the `.widget-heading` ruleset one level deeper than `.widget`. This is
useful information to developers that can now be gleaned just by a glance at the
indentation of our rulesets.
从中我们可以发现，`.widget-heading` 一定是 `.widget` 的子元素，因为前者比后者多缩进了一级。这使得开发者在阅读这些规则集时可以快速获取信息。

We can also see that `.widget-heading`’s declarations are ordered by their
relevance; `.widget-heading` must be a textual element so we begin with our
text rules, followed by everything else.
我们还可以看出 `.widget-heading` 的声明是根据其相关性排列的；`.widget-heading` 一定是个文字元素，所以我们先添加文字相关的样式声明，接下来是其它的。

One exception to our multi-line rule might be in cases of the following:
以下为一个不分成多行的例子：

    .t10    { width:10% }
    .t20    { width:20% }
    .t25    { width:25% }       /* 1/4 */
    .t30    { width:30% }
    .t33    { width:33.333% }   /* 1/3 */
    .t40    { width:40% }
    .t50    { width:50% }       /* 1/2 */
    .t60    { width:60% }
    .t66    { width:66.666% }   /* 2/3 */
    .t70    { width:70% }
    .t75    { width:75% }       /* 3/4*/
    .t80    { width:80% }
    .t90    { width:90% }

In this example (from [inuit.css’s table grid system](
https://github.com/csswizardry/inuit.css/blob/master/inuit.css/partials/base/_tables.scss#L88))
it makes more sense to single-line our CSS.
这个例子（来自[inuit.css’s table grid system](https://github.com/csswizardry/inuit.css/blob/master/inuit.css/partials/base/_tables.scss#L88)）中将 CSS 放在一行将使得代码更紧凑。

## Naming conventions 命名规范

For the most part I simply use hyphen delimited classes (e.g. `.foo-bar`, not
`.foo_bar` or `.fooBar`), however in certain circumstances I use BEM (Block,
Element, Modifier) notation.
一般情况下我都是以连字符（-）连接 class 的名字（例如 `.foo-bar` 而非 `.foo_bar` 或 `.fooBar`），不过在某些特定的时候我会用 BEM（Block, Element, Modifier）命名法。

<abbr title="Block, Element, Modifier">BEM</abbr> is a methodology for naming
and classifying CSS selectors in a way to make them a lot more strict,
transparent and informative.
<abbr title="Block, Element, Modifier">BEM</abbr> 命名法可以使得选择器更规范，更透明，更具语义化。

The naming convention follows this pattern:
该命名法按照如下格式：

    .block{}
    .block__element{}
    .block--modifier{}

* `.block` represents the higher level of an abstraction or component.
* `.block__element` represents a descendent of `.block` that helps form `.block`
  as a whole.
* `.block--modifier` represents a different state or version of `.block`.

* `.block` 代表某个顶层抽象元素；
* `.block__element` 代表 `.block` 的一个子元素；
* `.block--modifier` 代表 `.block` 某个状态不同的版本。

An **analogy** of how BEM classes work might be:
一份 BEM **结构** 大致如下：

    .person{}
    .person--woman{}
        .person__hand{}
        .person__hand--left{}
        .person__hand--right{}

Here we can see that the basic object we’re describing is a person, and that a
different type of person might be a woman. We can also see that people have
hands; these are sub-parts of people, and there are different variations,
like left and right.
这个例子中我们描述的最基本元素是一个人，然后这个人的某个不同状态可能是一个女人。我们都知道人拥有手，这些是人体的一部分，而手也有不同的状态，如同左手与右手。

We can now namespace our selectors based on their base objects and we can also
communicate what job the selector does; is it a sub-component (`__`) or a
variation (`--`)?
这样我们就可以根据选择器的父元素来规定其命名空间并传达该选择器的职能，它是一个子元素（`__`）还是其他状态（`--`）？

So, `.page-wrapper` is a standalone selector; it doesn’t form part of an
abstraction or a component and as such it named correctly. `.widget-heading`,
however, _is_ related to a component; it is a child of the `.widget` construct
so we would rename this class `.widget__heading`.
由此，`.page-wrapper` 是一个单独的选择器，这个命名是正确的而且它也不是其它元素的子元素或其它状态；然而 `.widget-heading` 则与其它对象 _相关_  ，它应当是 `.widget` 的子元素，所以我们应当将该 class 重命名为 `.widget__heading`。

BEM looks a little uglier, and is a lot more verbose, but it grants us a lot of
power in that we can glean the functions and relationships of elements from
their classes alone. Also, BEM syntax will typically compress (gzip) very well
as compression favours/works well with repetition.
BEM 命名法虽然不太好看，而且相当冗长，但是它使得我们可以仅仅通过名称便快速获知元素的功能和元素之间的关系。与此同时，BEM 语法中的重复部分非常有利于压缩算法。

Regardless of whether you need to use BEM or not, always ensure classes are
sensibly named; keep them as short as possible but as long as necessary. Ensure
any objects or abstractions are very vaguely named (e.g. `.ui-list`, `.media`)
to allow for greater reuse. Extensions of objects should be much more explicitly
named (e.g. `.user-avatar-link`). Don’t worry about the amount or length of
classes; gzip will compress well written code _incredibly_ well.
无论你是否使用 BEM 命名法，你都应当确保 class 命名得当，力保一字不多、一字不少；确保元素命名抽象化以提高可复用性（例如 `.ui-list`，`.media`）。由此拓展出去的元素命名则要尽量精准（例如 `.user-avatar-link`）。不用担心 class 名的数量或长度，因为写得好的代码 gzip 也能_有效_ 压缩。

### Classes in HTML HTML 中的 class

In a bid to make things easier to read, separate classes is your HTML with two
(2) spaces, thus:
为了确保易读性，在 HTML 中用两个空格隔开 class 名，例如：

    <div class="foo--bar  bar__baz">

This increased whitespace should hopefully allow for easier spotting and reading
of multiple classes.
增加的空格应当可以使得在使用多个 class 时更易阅读与定位。

### JS hooks JS 钩子

**Never use a CSS _styling_ class as a JavaScript hook.** Attaching JS behaviour
to a styling class means that we can never have one without the other.
**千万不要把 CSS _样式_ 用作 JavaScript 钩子。** 把 JS 行为跟样式连在一起将无法分别处理。

If you need to bind to some markup use a JS specific CSS class. This is simply a
class namespaced with `.js-`, e.g. `.js-toggle`, `.js-drag-and-drop`. This means
that we can attach both JS and CSS to classes in our markup but there will never
be any troublesome overlap.
如果你要把 JS 和某些标记绑定起来的话，写一个 JS 专用的 CSS class。简单地说就是一个前缀 `.js-` 的明明空间，例如 `.js-toggle`，`.js-drag-and-drop`。这意味着我们可以在 class 上同时绑定 JS 和 CSS 而不会因为重复而引发麻烦。

    <th class="is-sortable  js-is-sortable">
    </th>

The above markup holds two classes; one to which you can attach some styling for
sortable table columns and another which allows you to add the sorting
functionality.
上面的这个标记有两个 class，你可以用其中一个来给这个可排序的表格栏添加样式，用另一个添加排序功能。

### Internationalisation i18n

Despite being a British developer—and spending all my life writing <i>colour</i>
instead of <i>color</i>—I feel that, for the sake of consistency, it is better
to always use US-English in CSS. CSS, as with most (if not all) other languages,
is written in US-English, so to mix syntax like `color:red;` with classes like
`.colour-picker{}` lacks consistency. I have previously suggested and advocated
writing bilingual classes, for example:
虽然我（该 CSS Guideline 文档原作者 Harry Roberts）是个英国人，而且我一向拼写 <i>colour</i> 而非 <i>color</i>，但是为了统一性，我认为在 CSS 中用美式拼法更佳。CSS 以及其它多数语言都是以美式拼法写就，所以在 `.colour-picker{}` 中写 `color:red` 就缺乏统一性。我之前主张同时用两种拼法，例如：

    .color-picker,
    .colour-picker{
    }

However, having recently worked on a very large Sass project where there were
dozens of colour variables (e.g. `$brand-color`, `$highlight-color` etc.),
maintaining two versions of each variable soon became tiresome. It also means
twice as much work with things like find and replace.
但是我最近参与了一份非常巨大的 Sass 项目，这个项目中有许多的色彩变量（例如 `$brand-color`，`$highlight-color` 等等），每个变量要维护两种拼法实在辛苦，要查找并替换时也要两倍的工作量。

In the interests of consistency, always name classes and variables in the locale
of the language you are working with.
所以为了统一性，把所有的 class 与变量都以你参与的项目的管用拼法命名即可。

## Comments 注释

I use a docBlock-esque commenting style which I limit to 80 characters in length:
我使用行宽不超过 80 字节的块状注释：

    /**
     * This is a docBlock style comment
     * 
     * This is a longer description of the comment, describing the code in more
     * detail. We limit these lines to a maximum of 80 characters in length.
     * 
     * We can have markup in the comments, and are encouraged to do so:
     * 
       <div class=foo>
           <p>Lorem</p>
       </div>
     * 
     * We do not prefix lines of code with an asterisk as to do so would inhibit
     * copy and paste.
     */

    /**
     * 是为块状注释
     *
     * 这部分是描述更详细、篇幅更长的注释。当然，我们要把行宽压在 80 字以内。
     *
     * 我们可以在注释中嵌入 HTML 标记，而且这也是个好办法：
     *
        <div class=foo>
            <p>Lorem</p>
        </div>
     *
     * 如果是注释内嵌的标记的话，我们前面不加星号，否则容易被复制进去。
     */

You should document and comment our code as much as you possibly can, what may
seem or feel transparent and self explanatory to you may not be to another dev.
Write a chunk of code then write about it.
在注释中尽量详细描述代码，因为对你来说显然的内容对其他人可能并非如此。每写一部分代码就要专门写注释以详解。

### Comments on steroids 更好的用法

There are a number of more advanced techniques you can employ with regards
comments, namely:
在注释中有许多非常好的方法，例如：

* Quasi-qualified selectors
* Tagging code
* Object/extension pointers

* 准修饰选择器
* 代码标签
* 继承标记

#### Quasi-qualified selectors 准修饰选择器

You should never qualify your selectors; that is to say, we should never write
`ul.nav{}` if you can just have `.nav`. Qualifying selectors decreases selector
performance, inhibits the potential for reusing a class on a different type of
element and it increases the selector’s specificity. These are all things that
should be avoided at all costs.
你应当避免过分修饰选择器，例如如果你能写 `.nav{}` 的话就尽量不要写 `ul.nav{}`。过分修饰选择器将影响性能，影响 class 重用性，增加选择器专有度。这些都是你应当尽力避免的。

However, sometimes it is useful to communicate to the next developer(s) where
you intend a class to be used. Let’s take `.product-page` for example; this
class sounds as though it would be used on a high-level container, perhaps the
`html` or `body` element, but with `.product-page` alone it is impossible to
tell.
不过有时告诉其它开发者你希望 class 用在哪里倒是非常有效。以 `.product-page` 为例，这个 class 听起来像是一个高级别的容器，可能是 `html` 或者 `body` 元素，但是只有一个 `.product-page` 就无法判断。

By quasi-qualifying this selector (i.e. commenting out the leading type
selector) we can communicate where we wish to have this class applied, thus:
我们可以在选择器前加上准修饰（即将前面的类型选择器注释掉）来描述我们希望的 class 作用元素：

    /*html*/.product-page{}

We can now see exactly where to apply this class but with none of the
specificity or non-reusability drawbacks.
这样我们就能准确获知该 class 的作用范围而不会影响复用性。

Other examples might be:
其它例子如：

    /*ol*/.breadcrumb{}
    /*p*/.intro{}
    /*ul*/.image-thumbs{}

Here we can see where we intend each of these classes to be applied without
actually ever impacting the specificity of the selectors.
这样我们就能在不影响代码专有度的前提下获知 class 作用范围。

#### Tagging code 代码标签

If you write a new component then leave some tags pertaining to its function in
a comment above it, for example:
如果你写了一个新成员的话，可以在它上面加上标签，例如：

    /**
     * ^navigation ^lists
     */
    .nav{}
    
    /**
     * ^grids ^lists ^tables
     */
    .matrix{}

These tags allow other developers to find snippets of code by searching for
function; if a developer needs to work with lists they can run a find for
`^lists` and find the `.nav` and `.matrix` objects (and possibly more).
这些标签可以使得其他开发者快速找到相关代码。如果一个开发者需要查找和列表相关的部分，他只要搜索 `^lists` 就能快速定位到 `.nav`，`.matrix` 以及其它可能存在的。

#### Object/extension pointers 继承标记

When working in an object oriented manner you will often have two chunks of CSS
(one being the skeleton (the object) and the other being the skin (the
extension)) that are very closely related, but that live in very different
places. In order to establish a concrete link between the object and its
extension with use <i>object/extension pointers</i>. These are simply comments
which work thus:

以面向对象的思路来干活的话，你经常能找到两块 CSS 密切相关（其一为骨，其一为皮）却分列两处。我们可以用继承标记来在原元素和继承元素之间建立紧密联系。这些在注释中的写法如下：

In your base stylesheet:
在元素的基本样式表中：

    /**
     * Extend `.foo` in theme.css
     */
     .foo{}

In your theme stylesheet:
在元素的装饰样式表中：

    /**
     * Extends `.foo` in base.css
     */
     .bar{}

Here we have established a concrete relationship between two very separate
pieces of code.
这样一来我们就能在两块相隔很远的代码间建立紧密联系。

---

## Writing CSS 编写 CSS

The previous section dealt with how we structure and form our CSS; they were
very quantifiable rules. The next section is a little more theoretical and deals
with our attitude and approach.
之前的章节主要探讨如何规划 CSS，这些都是易于量化的规则。本章将探讨更理论化的东西，也将探讨我们的态度与方法。

## Building new components 编写新组件

When building a new component write markup **before** CSS. This means you can
visually see which CSS properties are naturally inherited and thus avoid
reapplying redundant styles.
编写新组件时，要在 CSS **之前** 写好标记部分。这意味着你可以准确判断哪些 CSS 属性可以继承，避免重复浪费。

By writing markup first you can focus on data, content and semantics and then
apply only the relevant classes and CSS _afterwards_.  
先写标记的话，你就可以关注数据、内容与语义，__在这之后__ 再施加需要的 class 和 CSS 样式。

## OOCSS 面向对象 CSS

I work in an OOCSS manner; I split components into structure (objects) and
skin (extensions). As an **analogy** (note, not example) take the following:
我以面向对象 CSS 的方式携带吗。我把元素分成结构（对象）与外观（拓展）。正如以下解析（这个只是笔记而非例子）：

    .room{}
    
    .room--kitchen{}
    .room--bedroom{}
    .room--bathroom{}

We have several types of room in a house, but they all share similar traits;
they all have floors, ceilings, walls and doors. We can share this information
in an abstracted `.room{}` class. However we have specific types of room that
are different from the others; a kitchen might have a tiled floor and a bedroom
might have carpets, a bathroom might not have a window but a bedroom most likely
will, each room likely has different coloured walls. OOCSS teaches us to
abstract the shared styles out into a base object and then _extend_ this
information with more specific classes to add the unique treatment(s).
我们在屋子里有许多房间，不过它们都有相同的特点：他们都有地板、天花板、墙壁和门。这些共享的部分我们可以放到一个抽象的 `.room{}` class 中。不过我们还有其它与众不同的房间：一个厨房可能有地砖，卧室可能有地毯，洗手间可能没有窗户但是卧室会有，每个房间的墙壁颜色也许也会不一样。面向对象 CSS 的思路使得我们把相同部分抽象出来组成结构部分，然后用更具体的 class 来 _拓展_ 这些特征并添加特殊的处理方法。

So, instead of building dozens of unique components, try and spot repeated
design patterns across them all and abstract them out into reusable classes;
build these skeletons as base ‘objects’ and then peg classes onto these to
extend their styling for more unique circumstances.
所以比起编写大量的特殊模块，应当努力找出这些模块中重复的设计模式并将其抽象出来，写成一个可以复用的 class。把它们用作基础然后拓展其它模块的特殊情形。

If you have to build a new component split it into structure and skin; build the
structure of the component using very generic classes so that we can reuse that
construct and then use more specific classes to skin it up and add design
treatments.
当你要编写一个新组件时，将其拆分成结构和外观。编写结构部分时用最通用 class 以保证重用性，编写外观时用更具体的 class 来添加设计方法。

## Layout 布局

All components you build should be left totally free of widths; they should
always remain fluid and their widths should be governed by a parent/grid system.
你写的所有组件都不要规定宽度，而由父元素或 grid system 来规定。

Heights should **never** be be applied to elements. Heights should only be 
applied to things which had dimensions _before_ they entered the site (i.e.
images and sprites). Never ever set heights on `p`s, `ul`s, `div`s, anything.
You can often achieve the desired effect with `line-height` which is far more
flexible.
**坚决不要** 写 `height`。高度应当仅仅用于尺寸已经固定的东西，例如图片和 CSS Sprite。在 `p`，`ul`，`div` 等元素上千万别规定高度。想要规定的话就写 `line-height`，这个更加灵活。

Grid systems should be thought of as shelves. They contain content but are not
content in themselves. You put up your shelves then fill them with your stuff.
By setting up our grids separately to our components you can move components
around a lot more easily than if they had dimensions applied to them; this makes
our front-ends a lot more adaptable and quick to work with.

You should never apply any styles to a grid item, they are for layout purposes
only. Apply styling to content _inside_ a grid item. Never, under _any_
circumstances, apply box-model properties to a grid item.
你在 Grid System 上不应当添加任何样式，他们仅仅是为布局而用。在 Grid System _之中_ 再添加样式。在 Grid System 中任何情况下都不要添加盒模型相关属性。

## Sizing UIs UI 尺寸

I use a combination of methods for sizing UIs. Percentages, pixels, ems, rems
and nothing at all.
我用很多方法设定 UI 尺寸，包括百分比，`px`，`em`，`rem` 以及干脆什么都不用。

Grid systems should, ideally, be set in percentages. Because I use grid systems
to govern widths of columns and pages, I can leave components totally free of
any dimensions (as discussed above).
理想情况下，Grid System 应当用百分比设定。因为我用 Grid System 来固定栏宽和页宽，所以我可以不用理会元素的尺寸。

Font sizes I set in rems with a pixel fallback. This gives the accessibility
benefits of ems with the confidence of pixels. Here is a handy Sass mixin to
work out a rem and pixel fallback for you (assuming you set your base font
size in a variable somewhere):
我用 rem 定义字号，并且辅以 px 以兼容旧浏览器。这可以兼具 em 和 px 的优势。下面是一个非常漂亮的 Sass Mixin，假设你在别处声明了基本字号的话，用它就可以生成 rem 以及兼容旧浏览器的 px。

    @mixin font-size($font-size){
        font-size:$font-size +px;
        font-size:$font-size / $base-font-size +rem;
    }

I only use pixels for items whose dimensions were defined before the came into
the site. This includes things like images and sprites whose dimensions are
inherently set absolutely in pixels.
我只在已经固定尺寸的元素上使用 px，包括图片以及尺寸已经用 px 固定的 CSS Sprite。

### Font sizing 字号

I define a series of classes akin to a grid system for sizing fonts. These
classes can be used to style type in a double stranded heading hierarchy. For a
full explanation of how this works please refer to my article
[Pragmatic, practical font-sizing in CSS](http://csswizardry.com/2012/02/pragmatic-practical-font-sizing-in-css)

## Shorthand

**Shorthand CSS needs to be used with caution.**

It might be tempting to use declarations like `background:red;` but in doing so
what you are actually saying is ‘I want no image to scroll, aligned top-left,
repeating X and Y, and a background colour of red’. Nine times out of ten this
won’t cause any issues but that one time it does is annoying enough to warrant
not using such shorthand. Instead use `background-color:red;`.

Similarly, declarations like `margin:0;` are nice and short, but
**be explicit**. If you actually only really want to affect the margin on
the bottom of an element then it is more appropriate to use `margin-bottom:0;`.

Be explicit in which properties you set and take care to not inadvertently unset
others with shorthand. E.g. if you only want to remove the bottom margin on an
element then there is no sense in setting all margins to zero with `margin:0;`.

Shorthand is good, but easily misused.

## IDs

A quick note on IDs in CSS before we dive into selectors in general.

**NEVER use IDs in CSS.**

They can be used in your markup for JS and fragment identifiers but use only
classes for styling. You don’t want to see a single ID in any stylesheets!

Classes come with the benefit of being reusable (even if we don’t want to, we
can) and they have a nice, low specificity. Specificity is one of the quickest
ways to run into difficulties in projects and keeping it low at all times is
imperative. An ID is **255** times more specific than a class, so never ever use
them in CSS _ever_.

## Selectors

Keep selectors short, efficient and portable.

Heavily location-based selectors are bad for a number of reasons. For example,
take `.sidebar h3 span{}`. This selector is too location-based and thus we
cannot move that `span` outside of a `h3` outside of `.sidebar` and maintain
styling.

Selectors which are too long also introduce performance issues; the more checks
in a selector (e.g. `.sidebar h3 span` has three checks, `.content ul p a` has
four), the more work the browser has to do.

Make sure styles aren’t dependent on location where possible, and make sure
selectors are nice and short.

Selectors as a whole should be kept short (e.g. one class deep) but the class
names themselves should be as long as they need to be. A class of `.user-avatar`
is far nicer than `.usr-avt`.

**Remember:** classes are neither semantic or insemantic; they are sensible or
insensible! Stop stressing about ‘semantic’ class names and pick something
sensible and futureproof.

### Over-qualified selectors

As discussed above, qualified selectors are bad news.

An over-qualified selector is one like `div.promo`. You could probably get the
same effect from just using `.promo`. Of course sometimes you will _want_ to
qualify a class with an element (e.g. if you have a generic `.error` class that
needs to look different when applied to different elements (e.g.
`.error{ color:red; }` `div.error{ padding:14px; }`)), but generally avoid it
where possible.

Another example of an over-qualified selector might be `ul.nav li a{}`. As
above, we can instantly drop the `ul` and because we know `.nav` is a list, we
therefore know that any `a` _must_ be in an `li`, so we can get `ul.nav li a{}`
down to just `.nav a{}`.

### Selector performance

Whilst it is true that browsers will only ever keep getting faster at rendering
CSS, efficiency is something you could do to keep an eye on. Short, unnested
selectors, not using the universal (`*{}`) selector as the key selector, and
avoiding more complex CSS3 selectors should help circumvent these problems.

## CSS selector intent

Instead of using selectors to drill down the DOM to an element, it is often best
to put a class on the element you explicitly want to style. Let’s take a
specific example with a selector like `.header ul{}`…

Let’s imagine that `ul` is indeed the main navigation for our website. It lives
in the header as you might expect and is currently the only `ul` in there;
`.header ul{}` will work, but it’s not ideal or advisable. It’s not very future
proof and certainly not explicit enough. As soon as we add another `ul` to that
header it will adopt the styling of our main nav and the the chances are it
won’t want to. This means we either have to refactor a lot of code _or_ undo a
lot of styling on subsequent `ul`s in that `.header` to remove the effects of
the far reaching selector.

Your selector’s intent must match that of your reason for styling something;
ask yourself **‘am I selecting this because it’s a `ul` inside of `.header` or
because it is my site’s main nav?’**. The answer to this will determine your
selector.

Make sure your key selector is never an element/type selector or
object/abstraction class. You never really want to see selectors like
`.sidebar ul{}` or `.footer .media{}` in our theme stylesheets.

Be explicit; target the element you want to affect, not its parent. Never assume
that markup won’t change. **Write selectors that target what you want, not what
happens to be there already.**

For a full write up please see my article
[Shoot to kill; CSS selector intent](http://csswizardry.com/2012/07/shoot-to-kill-css-selector-intent/)

## `!important`

It is okay to use `!important` on helper classes only. To add `!important`
preemptively is fine, e.g. `.error{ color:red!important }`, as you know you will
**always** want this rule to take precedence.

Using `!important` reactively, e.g. to get yourself out of nasty specificity
situations, is not advised. Rework your CSS and try to combat these issues by
refactoring your selectors. Keeping your selectors short and avoiding IDs will
help out here massively.

## Magic numbers and absolutes

A magic number is a number which is used because ‘it just works’. These are bad
because they rarely work for any real reason and are not usually very
futureproof or flexible/forgiving. They tend to fix symptoms and not problems.

For example, using `.dropdown-nav li:hover ul{ top:37px; }` to move a dropdown
to the bottom of the nav on hover is bad, as 37px is a magic number. 37px only
works here because in this particular scenario the `.dropdown-nav` happens to be
37px tall.

Instead you should use `.dropdown-nav li:hover ul{ top:100%; }` which means no
matter how tall the `.dropdown-nav` gets, the dropdown will always sit 100% from
the top.

Every time you hard code a number think twice; if you can avoid it by using
keywords or ‘aliases’ (i.e. `top:100%` to mean ‘all the way from the top’)
or&mdash;even better&mdash;no measurements at all then you probably should.

Every hard-coded measurement you set is a commitment you might not necessarily
want to keep.

## Conditional stylesheets

IE stylesheets can, by and large, be totally avoided. The only time an IE
stylesheet may be required is to circumvent blatant lack of support (e.g. PNG
fixes).

As a general rule, all layout and box-model rules can and _will_ work without an
IE stylesheet if you refactor and rework your CSS. This means you never want to
see `<!--[if IE 7]> element{ margin-left:-9px; } < ![endif]-->` or other such
CSS that is clearly using arbitrary styling to just ‘make stuff work’.

## Debugging

If you run into a CSS problem **take code away before you start adding more** in
a bid to fix it. The problem exists in CSS that is already written, more CSS
isn’t the right answer!

Delete chunks of markup and CSS until your problem goes away, then you can
determine which part of the code the problem lies in.

It can be tempting to put an `overflow:hidden;` on something to hide the effects
of a layout quirk, but overflow was probably never the problem; **fix the
problem, not its symptoms.**

## Preprocessors

Sass is my preprocessor of choice. **Use it wisely.** Use Sass to make your CSS
more powerful but avoid nesting like the plague! Nest only when it would
actually be necessary in vanilla CSS, e.g.

    .header{}
    .header .site-nav{}
    .header .site-nav li{}
    .header .site-nav li a{}

Would be wholly unnecessary in normal CSS, so the following would be **bad**
Sass:

    .header{
        .site-nav{
            li{
                a{}
            }
        }
    }

If you were to Sass this up you’d write it as:

    .header{}
    .site-nav{
        li{}
        a{}
    }
