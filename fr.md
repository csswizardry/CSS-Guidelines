---
layout: default
permalink: /fr/
---

<h1 class="hide">{{ site.title }}</h1>
<h2 class="alpha  site-title">{{ site.description_fr }}</h2>

## À propos de l'auteur

<cite>CSS Guidelines</cite> est écrit par votre serviteur, [Harry Roberts](http://csswizardry.com/work/). Je suis Consultant en Architecture Front-end originaire du Royaume-Uni, mais j'aide des entreprises à l'international à développer et maintenir des interfaces de qualité. Je suis d'ailleurs disponible.

<p class="text-center">
<a href="https://twitter.com/csswizardry" class="btn  btn--secondary"><span class="hide-palm">Suivez-moi sur </span>Twitter</a>
ou <a href="http://csswizardry.com/work/" class="btn">Embauchez<span class="hide-palm"> moi</span></a>
</p>

---

## Soutenez CSS Guidelines

<cite>CSS Guidelines</cite> fonctionne sous le modèle *payez-ce-que-vous-voulez*, à partir de 0$. Si <cide>CSS Guidelines</cide> vous plait et vous est utile, envisagez de [soutenir le projet](https://gumroad.com/l/JAgjq).

<p class="text-center">
<a href="https://gumroad.com/l/JAgjq" class="btn">Soutenez CSS Guidelines</a>
</p>

Soyez au courant de tous les changements, mises à jour et nouvelles sections en suivant [@cssguidelines](https://twitter.com/cssguidelines) sur Twitter.

---

## Contents

* [Introduction](#introduction)
    * [De l'importance d'un styleguide](#de-limportance-dun-styleguide)
    * [Avertissement](#avertissement)
* [Syntaxe et formatage](#syntaxe-et-formatage)
    * [Multiples fichiers](#multiples-fichiers)
    * [Table des matières](#table-des-matires)
    * [Limite de 80 caractères](#des-lignes-de-80-caractres)
    * [Titres](#titres)
    * [Anatomie d'une règle CSS](#anatomie-dune-rgle-css)
    * [CSS multi-lignes](#css-multi-lignes)
    * [Indentation](#indentation)
        * [Indentation avec Sass](#indentation-sass)
        * [Alignement](#alignement)
    * [De l'intérêt des espaces](#gestion-des-espaces)
    * [HTML](#html)
* [Commentaire](#commentaires)
    * [Général](#gnral)
        * [Pointeur Objet–Extension](#pointeur-objet-extension)
    * [Spécifique](#spcifique)
    * [Commentaires de pré-processeurs](#commentaires-de-pr-processeur)
    * [Retirer les commentaires](#retrait-des-commentaires)
* [Conventions de nommage](#conventions-de-nommage)
    * [Séparation par traits d'union](#sparation-par-traits-dunion)
    * [Notation BEM-like](#notation-bem-like)
        * [Contexte de départ](#contexte-de-dpart)
        * [Davantage de niveaux](#davantage-de-niveaux)
        * [Modifier les éléments](#modifier-les-lments)
    * [Conventions de nommage en HTML](#conventions-de-nommage-en-html)
    * [Ancres JavaScript](#ancres-javascript)
        * [Attributs `data-*`](#attributs-data-)
    * [Aller plus loin](#pour-aller-plus-loin-1)
* [Sélecteurs CSS](#slecteurs-css)
    * [Intention](#intention)
    * [Réutilisation](#rutilisation)
    * [Indépendance](#indpendance)
    * [Portabilité](#portabilit)
        * [Sélecteurs quasi-qualifié](#slecteurs-quasi-qualifis)
    * [Nommage](#nommage)
        * [Nommage des composants d'interface](#nommage-des-composants-dinterface)
    * [Performance des sélecteurs](#performance-des-slecteurs)
        * [Le sélecteur clé](#le-slecteur-cl)
    * [Règles générales](#rgles-gnrales)
* [Spécifité](#spcificit)
    * [Les IDs en CSS](#les-ids-en-css)
    * [Imbrication](#imbrication)
    * [`!important`](#important)
    * [Contourner les problèmes de spécificités](#contourner-les-problmes-de-spcificit)


### À venir

* Architecture
* Pré-processeurs
* Layout
* Performance
* Code déplorable
* Code obsolète, hacks et dette technique

---

## Introduction

CSS n'est pas un langage terrible. Bien qu'il soit simple de s'y mettre et d'apprendre à s'en servir, plus on écrit de CSS, plus la maintenance devient problématique. On ne peut pas changer la façon dont CSS fonctionne, mais on peut adapter la façon dont on l'utilise.

Quand on travaille sur des projets à grande échelle, qui durent, avec des dizaines de développeurs aux compétences différentes, il est important de travailler tous de la même manière afin de (entre autres) :

* garder des feuilles de styles maitenables ;
* garder un code clair et lisible ;
* faire en sorte que les feuilles de styles restent les plus légères possibles, quelle que soit la taille du projet.

Il y a un certain nombre de choses que l'on peut faire pour atteindre ces objectifs, et <cite>CSS Guidelines</cite> a justement pour but de nous aider à en arriver là.

### De l'importance d'un styleguide

Adopter des lignes de conduites en matière de code (on ne parle pas là d'un styleguide visuel donc) est primordiable pour les équipes qui :

* conçoivent et maintiennent des produits sur une durée raisonnable ;
* sont constituées de développeurs de multiples horizons et aux capacités variées ;
* sont constrituées de plusieurs développeurs travaillant sur un même projet à un moment donné ;
* accueillent de nouvelles têtes régulièrement.

Bien que ce genre de lignes de conduite soit généralement dédié aux équipes plus ou moins grandes sur des projets plus ou moins importants s'étalant sur des durées plus ou moins longues, tout développeur se doit de standardiser un minimum son code.

De bonnes lignes de conduites, quand suivies, permettront de :

* mettre en place un certain standard de qualité ;
* s'assurer de la cohérence du code ;
* offrir aux développeurs un sentiment de familiarité ;
* améliorer la productivité.

Les lignes de conduites doivent être apprises, comprises et mises en pratique en tout temps sur un projet qui en a, et toute dérogation doit être soigneusement justifiée.

### Avertissement

<cite>CSS Guidelines</cite> est *un* styleguide et non pas *le* styleguide. Ces lignes de conduites contiennent de la méthodologie, des techniques et des conseils que je recommande fortement mais vos préférences et surtout le contexte de votre projet peuvent en décider autrement.

Ce styleguide a un avis très arrêté sur un certain nombre de choses, mais sachez qu'il a été essayé, testé, amélioré, poli, peaufiné et revisité au cours des années, sur des projets de toutes tailles.

---

## Syntaxe et formatage

Une des formes les plus simples de styleguide est tout simplement un ensemble de règles à propos de la syntaxe et du formatage du code. Avoir une façon bien standardisée d'écrire du code CSS, c'est s'assurer que n'importe quel développeur le comprenne et se sente en confiance avec celui-ci.

De plus, la propreté encourage la propreté. Du code propre constitue un environnement sain dans lequel travailler, qui encourage les développeurs à maintenir cette propreté. A l'inverse, du code de mauvaise qualité ne peut être que néfaste pour la maintenance.

De manière très schématique, on désire :

* Une indentation à quatre (4) espaces, pas de tabulation ;
* Pas plus de 80 caractères par ligne ;
* Du CSS écrit sur plusieurs lignes ;
* Une utilisation efficace des lignes vides.

<span class="highlight" id="Did-you-see-this-bit?">Mais, comme pour tout, l'essentiel est surtout d'être cohérent du début à la fin.</span>

### Multiples fichiers

Grâce aux pré-processeurs toujours plus utilisés, les développeurs divisent de plus en plus souvent le code CSS dans de multiples fichiers.

Même dans le cas où l'on n'utilise pas de pré-processeur CSS, c'est une bonne idée de diviser le code en morceaux distincts, qui seront par la suite concaténés durant le processus de déploiement.

Si pour une raison ou pour une autre, vous ne divisez pas votre code CSS dans plusieurs fichiers, la section suivante risque de perdre de son intérêt.

### Table des matières

Une table des matières est assez pénible à maintenir, mais elle vaut définitivement le coût. Tenir une table des matières à jour demande un développeur consciencieux mais c'est un atout considérable pour la maintenance du code. Une table à jour confère un accès unique et complet sur tout ce qui se trouve en matière de CSS dans le projet, dans quel ordre et pour quoi faire.

Une table des matières donne l'intitulé des sections ainsi qu'une description de celles-ci, dans l'ordre. Par exemple :

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

Chaque élément de la table des matières est associé à une section et/ou à l'inclusion d'un fichier.

Naturellement, cette section serait bien plus imposante dans la majorité des projets, mais elle a le mérite de donner un bon aperçu de la façon dont est constitué le projet, et comment faire pour le maintenir.

### Des lignes de 80 caractères

Quand c'est possible, essayez de limiter la longueur des lignes à 80 caractères. Entre autres, pour les raisons suivantes :

* pouvoir ouvrir plusieurs fichiers côte à côte sans retour à la ligne ;
* pouvoir lire confortablement sur GitHub ou dans le terminal ;
* conférer une longueur de ligne confortable pour les commentaires.

<pre><code>/**
 * Je suis un long commentaire. Je décris, en détails, les CSS qui suivent. Je
 * suis si long que je dépasse largement la limite des 80 caractères aussi je
 * suis divisé sur plusieurs lignes.
 */</code></pre>

Il y aura nécessairement des exceptions à cette règle, notamment les URLs, les dégradés, et autres mais dans la mesure du possible on s'y tiendra.

### Titres

Débutez chacune des sections principales du projet avec un titre :

    /*------------------------------------*\
        #TITRE-DE-SECTION
    \*------------------------------------*/

    .selector {}

Le titre de la section est préfixé par un dièze (`#`) afin de faciliter les recherches ciblées (telles que `grep`) : au lieu de chercher <kbd>SECTION-TITLE</kbd> qui peut retourner un certain nombre de résultats, on peut chercher <kbd>#SECTION-TITLE</kbd>, qui ne devrait en retourner qu'un seul.

Pensez à laisser une ligne vide entre le titre et la prochaine ligne de code, quelle qu'elle soit (commentaire, sélecteur, variable...).

Dans le cas où vous travaillez sur un projet où chaque section est dans son propre fichier, le titre doit se trouver tout en haut de celui-ci. Si plusieurs sections se trouvent dans le même fichier, chaque titre doit être précédé de cinq (5) lignes vides. Cet espace vide couplé au titre permet de bien repérer le début d'une nouvelle section lors du défilement.

    /*------------------------------------*\
        #UNE-SECTION
    \*------------------------------------*/

    .selector {}





    /*------------------------------------*\
        #UNE-AUTRE-SECTION
    \*------------------------------------*/

    /**
     * Comment
     */

    .another-selector {}

{% include promo-buy.html %}

### Anatomie d'une règle CSS

Avant que l'on aille plus loin sur la façon dont on écrit nos règles, familiarisons-nous déjà avec la terminologie :

    [selector] {
        [property]: [value];
        [<--declaration--->]
    }

Par exemple :

    .foo, .foo--bar,
    .baz {
        display: block;
        background-color: green;
        color: red;
    }

Nous avons donc :

* les sélecteurs liés sur la même ligne, sinon sur une ligne différente ;
* un espace avant l'accolade ouvrante (`{`) ;
* l'accolade ouvrante (`{`) sur la ligne du dernier sélecteur ;
* chaque déclaration sur une même ligne ;
* chaque déclaration indentée de 4 espaces ;
* un espace après le deux-points (`:`) ;
* un point-virgule (`;`) à la dernière déclaration également ;
* l'accolade fermante (`}`) sur sa propre ligne.

Ce formatage est somme toute assez traditionel (à l'exception de l'indentation qui varie selon les développeurs).

De fait, le code suivant est considéré incorrect :

    .foo, .foo--bar, .baz
    {
      display:block;
      background-color:green;
      color:red }

On dénote les problèmes suivants :

* des tabulations au lieu d'espaces ;
* des sélecteurs non liés sur la même ligne ;
* l'accolade ouvrante (`{`) sur sa propre ligne ;
* l'accolade fermante (`}`) pas sur sa propre ligne ;
* le dernier point-virgule (`;`) manquant ;
* pas d'espace après les deux-points (`:`).

### CSS multi-lignes

Le code CSS doit être écrit sur plusieurs lignes, sauf en des circonstances bien particulières. L'intérêt d'utiliser plusieurs lignes est de :

* réduire les chances de conflits de merge (Git) car chaque fonctionnalité est contenue sur sa propre ligne ;
* des `diff`s (Git) plus fiables car une ligne ne subira jamais plus d'un changement.

Les exceptions à cette règle sont assez évidentes, notamment lorsqu'il y a de multiples règles successives qui ne contiennent qu'une déclaration. Par exemple :

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

Ces règles sont mieux sur une seule ligne car :

* elles sont toujours conformes au précepte un-changement-par-ligne ;
* elles sont suffisamment similaires pour être plus simples à lire de cette façon, surtout s'il s'agit de scanner visuellement les sélecteurs.

### Indentation

De la même manière que l'on indente les déclarations, on indente également les règles entières pour signaler leur relation avec d'autres. Par exemple :

    .foo {}

        .foo__bar {}

            .foo__baz {}

En faisant ça, un développeur peut voir d'un simple coup d'oeil que `.foo__baz` se trouve à l'intérieur de `.foo__bar` qui se trouve à l'intérieur de `.foo`.

Cette pseudo-réplication du DOM permet de savoir où sont supposées se trouver les classes sans avoir le HTML sous les yeux.

#### Indentation Sass

Sass permet d'imbriquer les sélecteurs les uns dans les autres. Par exemple, le code suivant :

    .foo {
        color: red;

        .bar {
            color: blue;
        }

    }

…va être compilé comme suit :

    .foo { color: red; }
    .foo .bar { color: blue; }

Même dans le cas de Sass, on s'en tient à quatre (4) espaces pour l'indentation. On laisse également une ligne vide avant et après la règle imbriquée.

***N.B.** L'imbrication des sélecteurs doit être évitée autant que faire se peut. Référez vous à [la section dédiée à la Spécificité](#spcificit) pour davantage de détails.

#### Alignement

Essayez de grouper et d'aligner les déclarations liées. Par exemple :

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

Ceci rend la vie légèrement plus simple pour les développeurs dont les éditeurs de texte supportent l'édition en colonne, leur permettant de changer plusieurs valeurs identiques en une fois.

### Gestion des espaces

Comme pour l'indentation, on peut donner beaucoup d'informations en utilisant judicieusement les espaces entre les règles. Or donc :

* une (1) ligne vide entre les règles fortement liées ;
* deux (2) lignes vides entre les règles plus ou moins liées ;
* cinq (5) lignes vides entre les sections.

Par exemple :

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

Il ne devrait jamais y avoir de cas où deux règles sont juxtaposées sans ligne vide entre elles. En outre, ce code serait incorrect :

    .foo {}
        .foo__bar {}
    .foo--baz {}

### HTML

Dans la mesure où HTML et CSS sont intimement liés, je me dois de présenter également quelques règles de syntaxe et de formatage pour le markup.

Mettez systématiquement les valeurs de vos attributs entre guillemets, même si ceux-ci sont optionnels. Ceci afin de réduire les risques d'accidents, d'autant que c'est généralement plus lisible. Donc bien que le code suivant fonctionne :

    <div class=box>

…on préférera :

    <div class="box">

Les guillemets ne sont pas obligatoires, mais il est préférable de les ajouter.

Lorsque vous renseignez plusieurs valeurs à l'attribut `class`, séparez-les par deux espaces comme ceci :

    <div class="foo  bar">

Quand plusieurs classes sont liées les unes aux autres, envisagez de les grouper avec des crochets (`[` et `]`) comme ceci :

    <div class="[ box  box--highlight ]  [ bio  bio--long ]">

Gardez à l'esprit que ce n'est pas une règle gravée dans le marbre et que c'est quelque chose que j'expérimente encore moi-même mais je dois dire qu'elle apporte un certain nombre d'avantages. Je vous invite à lire sur ce sujet dans mon article [<cite>Grouping related classes in your markup</cite>](http://csswizardry.com/2014/05/grouping-related-classes-in-your-markup/).

Comme pour le code CSS, il est possible d'utiliser les sauts de ligne dans notre HTML également. On peut donc dénoter clairement des changements de section en insérant cinq (5) lignes vides, comme suit :

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

Pensez à séparer les blocs indépendants mais liés avec une simple ligne vide pour améliorer la lisibilité :

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

Ceci permet aux développeurs de repérer les différentes parties du DOM au premier coup d'oeil, et également aux éditeurs tels que Vim par exemple de manipuler des blocs délimités par des lignes vides.

### Pour aller plus loin

* [<cite>Grouping related classes in your markup</cite>](http://csswizardry.com/2014/05/grouping-related-classes-in-your-markup/)

---

## Commentaires

Un projet CSS a tellement de spécificités qui lui sont propres que bien souvent, les développeurs se retrouvent dans le scénario cauchemar du *je-n'ai-pas-écrit-ce-code*. Autant il est possible de se souvenir de ses propres sélecteurs, objets, outils, et classes dans une moindre mesure, autant se souvenir de ceux de tous les acteurs du projet est à la limite de l'impossible.

**C'est pourquoi il faut impérativement commenter le code CSS.**

Parce que CSS est un langage déclaratif, il est parfois difficile de savoir, en se contentant de lire une feuille de styles :

* si une règle dépend d'autres règles définies ailleurs ;
* si les changements d'une règle auront des répercussions ailleurs ;
* si une règle est belle et bien utilisée ;
* de quels styles héritent une règle (de manière intentionnelle ou non) ;
* si l'auteur s'attendait à ce qu'une règle soit utilisée.

Et encore, on ne parle pas là des multiples excentricité de CSS comme les différentes valeurs de `overflow` qui déclenchent des contextes de formatage, ou certaines transformations qui forcent l'accélération matérielle. Bien des cas qui ne peuvent qu'étonner des développeurs arrivant sur le projet.

Donc dans la mesure où CSS est plutôt déplorable quand il s'agit d'être explicite, le langage bénéficie grandement de la présence de commentaires.

De fait, vous devriez commenter tout ce qui ne saute pas aux yeux immédiatement. Évidemment, il n'y a aucun intérêt à expliquer que `color: red` change la couleur du texte en rouge. Mais si vous utilisez `overflow: hidden` pour *clear* les *floats* et non pas pour empêcher l'affichage d'éventuels débordements, c'est probablement intéressant de le documenter.

### Général

Pour les longs commentaires qui documentent une section entière, on utilise un type DocBlock sur plusieurs lignes qui s'en tient à notre règle des 80 caractères par ligne.

Voilà un exemple tiré de la feuille de styles traitant de l'entête du site [CSS Wizardry](http://csswizardry.com/) :

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

Ce niveau de détail devrait être la norme pour n'importe quelle description non-triviale.

#### Pointeur Objet-Extension

En travaillant sur de multiples fichiers, par exemple dans le cas d'une approche OOCSS, il arrive souvent que des règles qui sont pourtant liées d'une manière ou d'une autre ne se trouvent pas dans le même fichier. Par exemple, on peut avoir un objet bouton très générique qui ne s'occupe que de la structure. Celui-ci est par la suite étendu par un composant qui va ajouter la partie cosmétique. On documente ce genre de relations avec ce que l'on appelle un *pointeur objet-extension*.

Par exemple, dans le fichier de l'objet :

    /**
     * Étend `.btn {}` dans _components.buttons.scss.
     */

    .btn {}

Et dans le thème :

    /**
     * Ces règles étendent `.btn {}` dans _objects.buttons.scss.
     */

    .btn--positive {}

    .btn--negative {}

Ce commentaire si simple peut vraiment faire la différence pour les développeurs qui ne sont pas familiarisés avec les différentes relations qui existent entre les composants du projet. Même chose quand il s'agit de comprendre pourquoi et comment des règles sont héritées par un objet.

### Spécifique

Souvent, il est question de commenter une déclaration bien spécifique. Pour se faire, on utilise une sorte de note de pied-de-page inversée. Voila un commentaire un peu plus complexe détaillant la large entête de site mentionnée plus haut :

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

Ce genre de commentaires nous permet de conserver toute la documentation d'une règle à un seul endroit tout en référant à des lignes bien spécifiques de ladite règle.

### Commentaires de pré-processeur

Avec la plupart, si ce n'est tous les pré-processeurs, on peut écrire des commentaires qui ne seront pas compilés dans la feuille de styles finale. La règle est d'utiliser ces commentaires pour ne documenter que des éléments qui ne sont pas compilés en CSS non plus, c'est à dire de la syntaxe spécifique au pré-processeur. Pour documenter du code qui est compilé, on utilise des commentaires CSS traditionnels.

Par exemple, ceci est correct :

    // Dimensions de l'image sprite @2x:
    $sprite-width:  920px;
    $sprite-height: 212px;

    /**
     * 1. La taille par défaut de l'icône est 16px.
     * 2. Redimensionne la sprite retina pour l'afficher à la bonne taille.
     */
    .sprite {
        width:  16px; /* [1] */
        height: 16px; /* [1] */
        background-image: url(/img/sprites/main.png);
        background-size: ($sprite-width / 2) ($sprite-height / 2); /* [2] */
    }

Ici, on documente des variables &mdash;donc du code qui n'est pas compilé en CSS&mdash; avec des commentaires de pré-processeur, alors que le code CSS &mdash;qui est lui compilé dans le fichier final&mdash; est commenté avec des commentaires CSS.

Cela signifie que l'on aura dans la feuille de styles uniquement les commentaires porteurs d'information vis à vis du code compilé.

### Retrait des commentaires

Cela va sans dire qu'aucun commentaire ne devrait se trouver dans un fichier CSS généré pour un environnement de production. Les feuilles de style doivent être minifiées et dépouillées de tout commentaire avant d'être déployées.

---

## Conventions de nommage

Respecter des conventions de nommage en CSS est très utile pour rendre le code plus strict, et par la même occasion plus transparent.

De bonnes conventions de nommage permettent de savoir :

* ce que fait une classe ;
* où une classe peut être utilisée ;
* à quoi une classe peut être liée.

Les conventions de nommage que je suggère sont très simples : des chaînes séparées par des traits d'union (`-`), avec une approche BEM-like pour des cas plus complexes.

Il est bon de préciser que ces conventions de nommage sont bien plus utiles en HTML qu'en CSS en réalité.

### Séparation par traits d'union

Toutes les chaînes de caractères dans les classes sont délimitées par des traits d'union (`-`), comme ceci :

    .page-head {}

    .sub-content {}

La notation *camel case* et l'utilisation des underscores (`_`) sont proscrites pour les classes communes. De fait, ceci est incorrect :

    .pageHead {}

    .sub_content {}

{% include promo-buy.html %}

### Notation BEM-like

Pour les cas plus complexes où des morceaux d'interface sont corrélés les uns aux autres, on utilise une notation dite *BEM-like*.

<cite>BEM</cite>, acronyme pour <i>Block Element Modifier</i>, est une méthodologie front-end mise au point par les développeurs de Yandex. BEM est une méthodologie complète à laquelle on emprunte uniquement ses conventions de nommage. De plus, on parle de BEM-*like* car bien que les principes soient exactement les mêmes, la syntaxe varie légèrement.

BEM divise les composents en trois groupes :

* Block : la racine d'un composant ;
* Element : un composant faisant partie de Block ;
* Modifier : une variante ou une extension de Block.

Pour faire une analogie (à défaut d'un exemple) :

    .personne {}
    .personne__tete {}
    .personne--grande {}

Les éléments (Element) sont délimités par deux underscores (`__`) et les modificateurs (Modifier) sont délimités par deux traits d'union (`--`).

Ici, on voit que `.personne` est le block (Block); c'est la racine d'une entité distincte. `.personne__tete` est un élément (Element); c'est une sous-partie du bloc `.personne`. Enfin, `.personne--grande` est un modificateur (Modifier); c'est une variante spécifique du bloc `.personne`.

#### Contexte de départ

Un contexte de bloc (Block) débute généralement à l'endroit indépendant le plus logique. Pour poursuivre sur notre analogie, on n'aurait pas `.piece__personne` parce qu'une pièce est un tout autre contexte, bien plus grand qui plus est. On va donc séparer les blocs de cette façon :

    .piece {}

        .piece__porte {}

    .piece--cuisine {}


    .personne {}

        .personne__tete {}

Si on veut cibler une personne (`.personne`) au sein d'une pièce (`.piece`), il serait plus correct d'utiliser un sélecteur tel que `.piece .personne`.

Un exemple plus réaliste pourrait ressembler à cela, où chaque bout de code représente son propre bloc (Block) :

    .page {}


    .content {}


    .sub-content {}


    .footer {}

        .footer__copyright {}

Une notation comme suit serait dont incorrecte :

    .page {}

        .page__content {}

        .page__sub-content {}

        .page__footer {}

            .page__copyright {}

Il est important de comprendre quand démarre et se termine un bloc BEM. La règle, c'est que BEM s'applique à une partie bien distincte de l'interface.

#### Davantage de niveaux

Si l'on veut ajouter un nouvel élément (Element) &mdash;par exemple, `.personne__oeil {}`&mdash; à notre composant `.personne`, on ne doit pas traverser tout le chemin du DOM. C'est à dire que la notation correcte est `.personne_°oeil {}` et non pas `.personne__tete__oeil {}`. Les classes n'ont pas pour vocation de représenter le DOM.

#### Modifier les éléments

Il est possible d'avoir des variantes de certains éléments, et celles-ci peuvent être écrites de bien des manières selon comment et pourquoi l'élément est modifié. Pour continuer avec l'exemple d'une personne, un oeil bleu peut être représenté ainsi :

    .personne__oeil--bleu {}

Dans ce cas, on modifie directement l'élément (Element) oeil de la personne.

Cependant, les choses peuvent rapidement gagner en complexité. Pardonnez-moi d'avance l'analogie un peu terre-à-terre, et considérez que l'on ait un visage qui soit splendide. Ce n'est pas la personne en elle-même qui est splendide, mais son visage : un visage splendide sur une personne standard. Auquel cas on écrit :

    .personne__visage--splendud {}

En revanche si la personne *est* splendide, et que l'on veut styler son visage à cause de ce trait physique, on a un visage normal sur une personne splendide. Du coup :

    .personne--splendide .personne__visage {}

C'est là une occasion pour laquelle on utiliserait un sélecteur descendant pour modifier un élément (Element) en fonction d'un modification (Modifier) du bloc (Block).

Avec Sass, on écrirait :

    .personne {}

        .personne__visage {

            .personne--splendide & {}

        }

    .personne--splendide {}

Remarquez que l'on n'a pas besoin d'ajouter `.personne__visage` devant `.personne--splendide {}` car on utilise l'imbrication des règles. Cela permet d'avoir toutes les règles à propos de `.personne__visage {}` au même endroit, ce qui est généralement une bonne pratique quand on imbrique les règles. Conservez tout votre contexte (ici `.personne__visage`) à un seul endroit.

### Conventions de nommage en HTML

Comme je l'ai dit précédemment, les conventions de nommage ne sont pas si utiles que ça en CSS. C'est surtout dans le markup qu'elles deviennent vitales. Prenez par exemple le HTML suivant ne respectant aucune convention spécifique :

    <div class="box  profile  pro-user">

        <img class="avatar  image" />

        <p class="bio">...</p>

    </div>

Dans quelle mesure les classes `box` et `profile` sont elles liées ? Dans quelle mesure les classes `profile` et `avatar` sont elles liées ? Sont-elles seulement liées ? Les classes `bio` et `pro-user` doivent-elles être au même niveau ? Les classes `image` et `profile` sont elles destinées à faire partie d'un même ensemble ? Peut-on utiliser `avatar` ailleurs ?

En se contentant de ce markup, il est très difficile de répondre à toutes ses questions. Maintenant si l'on applique nos conventions de nommage, ça change tout :

    <div class="box  profile  profile--is-pro-user">

        <img class="avatar  profile__image" />

        <p class="profile__bio">...</p>

    </div>

Là nous pouvons clairement voir quelles sont les classes qui sont liées et comment. On voit également quelles sont les classes que l'on ne peut pas utiliser hors d'un certain périmètre, et on voit quelles sont celles qui sont parfaitement recyclables partout.

### Ancres Javascript

Il est généralement déconseillé d'attacher simultanément des CSS et du JavaScript à une même classe HTML. Et pour cause, il devient impossible d'en retirer un sans retirer l'autre. C'est bien plus propre et transparent d'appliquer des écouteurs JavaScript sur des classes dédiées à cela.

Il m'est arrivé par le passé de faire du ménage dans du code CSS, pour me rendre compte que des fonctionnalités JavaScript avaient disparu parce qu'elles étaient liées à des classes sur lesquelles des styles étaient appliqués. Impossible d'avoir l'un sans l'autre en somme.

Typiquement, on va donc préfixer les classes dédiées au JavaScript par `js-`, par exemple :

    <input type="submit" class="btn  js-btn" value="Follow" />

Cela signifie qu'on peut tout à fait balader les styles `.btn` sans forcément le comportement lié à `.js-btn`.

#### Attributs `data-*`

Une pratique commune est d'utiliser les attributs `data-*` comme ancres pour le JavaScript, mais c'est inapproprié. Selon les spécifications, ces attributs sont destinés à <q>**stocker des données personnalisées** spécifiques à la page ou l'application</q>. Les attributs sont donc faits pour stocker des données, pas pour être ciblés comme ancres.

### Pour aller plus loin

Comme on l'a dit précédemment, les conventions sont finalement assez simples, et se divisent en trois groupes de classes.

Je ne peux que vous encourager à pousser vos conventions de nommage plus loin pour intégrer davantage de fonctionnalités. C'est personnellement quelque chose que j'affectionne beaucoup.

### A lire

* [<cite>MindBEMding – getting your head ’round BEM syntax</cite>](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)

---

## Sélecteurs CSS

Au risque de vous surprendre, les sélecteurs constituent l'aspect le plus fondamental et le plus critique quand il s'agit de maintenir du code CSS. Leur spécificité, portabilité et capacité de réutilisation ont un impact direct sur la façon dont la feuille de styles est utilisée, et sur les éventuels problèmes que l'on peut rencontrer.

### Intention

Quand on écrit du code CSS, il est important d'écrire des sélecteurs corrects, et de sélectionner les bons éléments pour les bonnes raisons. L'<i>intention</i> d'un sélecteur, c'est le fait de se décider sur ce que vous désirez styler, et comment vous aller vous y prendre pour sélectionner l'élément à styler. Par exemple, si vous désirez appliquer des styles au menu principal de votre site, un sélecteur comme celui-ci serait très imprudent :

    header ul {}

L'intention de ce sélecteur est de cibler les éléments `ul` dans un élément `header`, alors que le besoin est de cibler le menu principal. On a donc là une intention incorrecte : on peut avoir autant de `header` que l'on veut sur une page, et eux-mêmes peuvent contenir un nombre indeterminés de `ul` aussi un sélecteur comme celui-ci risque d'appliquer des styles bien spécifiques à un grand nombre d'éléments. Suite à cela, on devra donc écrire encore plus de CSS pour défaire les méfaits de ce sélecteur.

Une approche plus sage serait de faire :

     .site-nav {}

C'est un sélecteur non ambigü, explicite avec une intention claire. On cible le bon élément pour la bonne raison.

Les problèmes de sélecteurs constituent les plus grosses sources de problèmes au sein des projets CSS. Les sélecteurs trop gourmands qui appliquent des règles bien spécifiques à de vastes collections d'éléments causent des effets de bord indésirables et mènent à des feuilles de styles bancales, où les sélecteurs entrent en conflit les uns avec les autres.

CSS ne peut pas être contenu ou encapsulé, mais on peut mitiger les fuites en évitant d'écrire des sélecteurs trop larges : **les sélecteurs doivent être explicites et sensés pour ne cibler que ce qui doit être ciblé**.

### Réutilisation

Lorsque l'on construit des interfaces en matière de composants, la notion de réutilisation est capitale. On veut pouvoir déplacer, recycler, dupliquer et éditer les objets de manière transversale sur les projets.

Pour cela, on utilise quasiment exclusivement des classes. Les IDs, au delà d'être extrêmement spécifiques, ne peuvent être utilisées qu'une seule fois par document, contrairement aux classes qui peuvent être dupliquées à l'infini. Tous vos choix doivent être effectués dans l'optique de maintenir du code réutilisable.

### Indépendance

De par la nature versatile des interfaces et de la notion même de composant, il est préférable de styler les éléments en fonction de ce qu'ils sont, et non pas d'où ils sont. Les composants ne doivent pas être stylés en fonction de leur position, d'où la notion d'indépendance.

Prenons comme un exemple un bouton dit *call-to-action* que l'on habille via le sélecteur suivant :

    .promo a {}

Tout d'abord on note là une intention incorrecte : tous les liens au sein d'un élément `.promo` sont stylés comme des boutons, ce qui ne satisfait pas la demande. De plus, ce sélecteur n'est pas indépendant dans la mesure où on ne peut pas réutiliser ce bouton hors d'un élément affublé de la classe `.promo` car il est explicitement lié à cet endroit.

Un bien meilleur sélecteur serait :

    .btn {}

Cette classe seule peut être réutilisée à l'extérieur d'un bloc `.promo` et portera toujours les styles cohérents. C'est un meilleur sélecteur parce qu'il est portable, recyclable, n'a aucune dépendance et fait preuve d'une meilleure intention. **Un composant ne doit pas avoir à vivre un certain endroit pour avoir une certaine apparence.**

{% include promo-hire.html %}

### Portabilité

Réduire ou même retirer complètement les dépendances liées au positionnement permet de pouvoir placer les composants de manière plus libre, mais qu'en est-il de la possibilité de balader certaines classes au sein des composants ?

En effet, il est possible d'agir à un niveau beaucoup plus bas afin que rendre certains sélecteurs portables, au delà de simples composants. Par exemple :

    input.btn {}

Ceci est un sélecteur <i>qualifié</i> ; la chaîne `input` lie la classe aux éléments de type `input` de sorte que seuls ceux-ci soient éligibles. En omettant ce qualificatif, on fait en sorte de pouvoir réutiliser cette classe `.btn` sur d'autres éléments comme `a` ou `button`.

De par leur nature même, les sélecteurs qualifiés sont difficiles à réutiliser or chaque sélecteur que l'on écrit devrait pouvoir l'être autant que faire se peut.

Bien sur, il y a des circonstances autour desquelles vous voulez légitimement qualifier un sélecteur, comme pour appliquer des styles spécifiques à un sélecteur s'il porte une certaine classe. Par exemple :

    /**
     * Met un élément avec la classe `.error` en emphase.
     */
    .error {
        color: red;
        font-weight: bold;
    }

    /**
     * Si l'élement est une `div`, applique des styles de boîte.
     */
    div.error {
        padding: 10px;
        border: 1px solid;
    }

C'est là un exemple où un sélecteur qualifié est tout à fait justifié, mais je recommanderais malgré tout l'approche suivante :

    /**
     * Erreurs au niveau d'un contenu textuel.
     */
    .error-text {
        color: red;
        font-weight: bold;
    }

    /**
     * Éléments qui contiennent des erreurs.
     */
    .error-box {
        padding: 10px;
        border: 1px solid;
    }

Ceci permet d'appliquer `.error-box` à n'importe quel élément, et pas uniquement à une `div`. C'est toujours plus réutilisable qu'un sélecteur qualifié.

#### Sélecteurs quasi-qualifiés

Ce qui est bien avec les sélecteurs qualifiés, c'est qu'ils signalent sur quel type d'élément une classe est supposée se trouver. Par exemple :

    ul.nav {}

Ici, on voit que la classe `.nav` est supposée être utiliée sur un élément `ul`, et non pas sur un élément `nav` (ou autre). En utilisant un <i>sélecteur quasi-qualifié</i>, on peut continuer de garder cette information sans pour autant qualifier le sélecteur de manière explicite :

    /*ul*/.nav {}

En commentant le qualificatif, il reste lisible mais évite d'accroitre la spécificité du sélecteur.

### Nommage

Comme l'a si bien dit Phil Karlton, <q>il n'y a que deux choses difficiles en informatique : l'invalidation du cache, et le nommage des choses</q>.

Je ne dirai rien sur la première de ces deux disciplines, mais la seconde m'a donné du fil à retordre des années durant. Mon conseil quand il s'agit de nommer les éléments en CSS serait de choisir quelque chose de sensé, mais en même temps d'un tantinet ambigü : pensez toujours "réutilisation". Par exemple, au lieu de choisir une classe comme `.site-nav`, optez plutôt pour `.primary-nav` ; plutôt que `.footer-links`, préférez `.sub-links`.

La différence entre ces noms, c'est que le premier de chaque example est lié à un cas d'usage : on ne peut les utiliser que comme navigation du site, et liens du pied-de-page respectivement. En utilisant un nommage légèrement plus ambigü, on rend ces composants portables dans d'autres circonstances.

Pour citer Nicolas Gallagher, <q>lier le nommage directement au contenu rend l'architecture difficile à maintenir et les composants peu réutilisables par les autres développeurs</q>.

En somme on doit choisir des noms sensés &mdash;des classes comme `.border` ou `.red` sont bien évidemment à proscrire&mdash; mais en même temps on devrait éviter de décrire la nature exacte du contenu et/ou ses cas d'utilisation. **Utiliser une classe pour décrire le contenu est redondant puisque le contenu est déjà supposé se décrire lui-même**.

Le débat autour du nommage sémantique des classes a fait rage pendant des années, aussi il est important d'adopter une approche plus pragmatique quand il s'agit de nommer les éléments de manière efficace. Au lieu de se focaliser sur la "sémantique", on s'efforce de s'attacher davantage à la longévité des sélecteurs. On nomme avant tout pour faciliter la maintenance, pas pour le plaisir de donner un nom.

On nomme pour les développeurs qui passeront après, ce sont les seuls qui vont *lire* lesdites classes. Encore une fois, il est préférable de trouver des noms réutilisables et recyclables plutôt que des intitulés n'autorisant qu'un cas d'usage unique. Prenons un exemple :

    /**
     * Risque d'être obsolète ; peu maintenable.
     */
    .blue {
        color: blue;
    }

    /**
     * Dépend de la position.
     */
    .header span {
        color: blue;
    }

    /**
     * Trop spécifique ; peu réutilisable.
     */
    .header-color {
        color: blue;
    }

    /**
     * Correctement abstrait, peu de chances de devenir obsolète et facilement réutilisable.
     */
    .highlight-color {
        color: blue;
    }

Il faut parvenir à trouver le juste milieu entre la description non-explicite des styles appliqués et la description non-spécifique du sens. Au lieu de `.home-page-panel`, on peut envisager `.masthead`. Au lieu de `.site-nav`, on favorise `.primary-nav`. Au lieu de `.btn-login`, on utilise `.btn-primary`.

#### Nommage des composants d'interface

Nommer les composants de manière agnostique et réutilisable aide les développeurs à construire et maintenir des interfaces plus rapidement et plus facilement. Cependant, il peut parfois être intéressant de spécifier des noms plus explicites à côté des classes parfois ambigües, surtout quand un certain nombre de classes très agnostiques viennent se grouper pour former un composant. Dans ce cas, avoir un nom éloquent s'avère utile.

Dans ce scénario, on accompagne les classes d'un attribut `data-ui-component` qui contient un nom plus spécifique. Par exemple :

    <ul class="tabbed-nav" data-ui-component="Main Nav">

On a donc les avantages d'une classe hautement réutilisable qui ne décrit pas de manière explicite le composant, et à la fois un nom plus parlant grâce à l'attribut `data-ui-component`. La valeur de ce dernier peut prendre n'importe quel format, comme celui d'un titre :

    <ul class="tabbed-nav" data-ui-component="Main Nav">

D'une classe :

    <ul class="tabbed-nav" data-ui-component="main-nav">

Ou d'un namespace :

    <ul class="tabbed-nav" data-ui-component="nav-main">

L'implémentation est essentiellement guidée par les préférences de chacun, mais le concept reste le même : **on ajoute du sens via un mécanisme qui n'entrave pas le caractère réutilisable des composants**.

### Performance des sélecteurs

Un sujet qui se trouve être plus intéressant qu'important compte tenu de la puissance des navigateurs d'aujourd'hui est celui de la performance des sélecteurs. C'est-à-dire la vitesse à laquelle le navigateur est capable de cibler les éléments du DOM à partir d'un sélecteur CSS.

De manière très générale, plus un sélecteur est long (comprendre plus il est fait de petits composants), plus il est lent. Par exemple :

    body.home div.header ul {}

…est bien moins efficace que :

    .primary-nav {}

Cela vient du fait que les navigateurs lisent les sélecteurs **de droite à gauche**. Un navigateur va donc lire le premier sélecteur de la façon suivante :

* trouver tous les `ul` du DOM ;
* puis tester s'ils se trouvent à l'intérieur d'un élément avec la classe `.header` ;
* puis tester que cette classe `.header` se trouve sur un élément de type `div` ;
* puis tester s'ils se trouvent à l'intérieur d'un élément avec la classe `.home` ;
* puis tester que cette classe `.home` se trouve sur un élément de type `body`.

Le deuxième sélecteur par contre :

* trouver tous les éléments qui ont la classe `.primary-nav`.

En d'autres termes, lorsque que l'on utilise des sélecteurs descendants (ex : `.foo .bar {}`), le navigateur commence par chercher la partie la plus à droite (`.bar`), puis remonte le DOM jusqu'à trouver la partie la plus à gauche (`.foo`). Cela peut impliquer de parcourir le DOM des dizaines de fois avant qu'un élément soit trouvé.

C'est une des raisons pour laquelle **imbriquer les sélecteurs avec un pré-processeur n'est pas une bonne idée**. Au delà de rendre les sélecteurs inutilement spécifiques, et de créer des dépendances de lieu, cela complique également le travail du navigateur.

En utilisant un sélecteur de descendance directe  (ex : `.foo > .bar {}`), on peut rendre le processus bien plus efficace car cela ne demande plus qu'un seul niveau de recherche pour le navigateur. Qu'il ait trouvé des éléments correspondants ou non, il cessera la recherche aussitôt le niveau du parent analysé.

#### Le sélecteur-clé

Parce que les navigateurs lisent les sélecteurs de droite à gauche, la partie la plus à droite d'un sélecteur est la plus critique vis à vis de la performance du sélecteur: c'est ce que l'on appelle le <i>sélecteur-clé</i>.

Le sélecteur suivant semble être extrêmement performant au premier coup d'oeil. Il utilise une ID, qui se trouve être très rapide, et dans la mesure où il ne peut y avoir qu'une occurrence par page, on est en droit d'estimer une exécution rapide. Après tout, il suffit de cibler l'élément avec l'ID recherchée et de styler tous ses enfants :

    #foo * {}

Le problème de ce sélecteur est que le sélecteur-clé (`*`) est très *très* gourmand. En réalité, ce sélecteur cible *tous les noeuds* du DOM (y compris `<title>`, `<link>`, `<head>`... absolument *tout*) puis teste s'ils font partie d'un élément avec l'ID `foo`. C'est donc un sélecteur *excessivement* coûteux qui devrait être évité dans la mesure du possible.

Heureusement, en écrivant des sélecteurs qui ont une [intention correcte](#intention), on évite justement ce genre de sélecteurs. On a rarement si ce n'est jamais de sélecteurs aussi gourmands, parce que l'on cible spécifiquement le(s) bon(s) élément(s) pour la bonne raison.

Ceci étant dit, la performance des sélecteurs devrait être le moindre de vos soucis en matière d'optimisation. Les navigateurs sont rapides, et ça va en s'arrangeant, aussi les cas où la performance d'un sélecteur se fait sentir sont exceptionnellement rares.

J'en profite pour rappeler qu'en plus des autres soucis qui leurs sont liés, l'imbrication, la qualification et les mauvaises intentions de sélecteurs contribuent aux éventuels problèmes de performance des sélecteurs.

### Règles générales

Vos sélecteurs constituent donc un critère fondamental dans l'écriture de code CSS efficace. Pour résumer très brièvement les sections précédentes :

* **On sélectionne explicitement ce que l'on veut** plutôt que de se baser sur des circonstances et la coïncidence. Maîtrise l'intention des sélecteurs est capitale.
* **On écrit des sélecteurs pour la réutilisation**, afin de limiter les pertes et la répétition.
* **On imbrique les sélecteurs que si ça fait sens**, car ça augmente la spécificité et entrave la réutilisation.
* **On évite la qualification des sélecteurs**, car là encore, cela vient empiéter sur la réutilisation des styles.
* **On essaye de garder des sélecteurs aussi courts que possible**, afin de limiter la spécificité et d'améliorer les performances.

Se focaliser sur tous ces points a pour effet de garder des sélecteurs sains et avec lesquels il est facile de travailler, y compris sur un projet à long terme.

### A lire pour aller plus loin

* [<cite>Shoot to kill; CSS selector intent</cite>](http://csswizardry.com/2012/07/shoot-to-kill-css-selector-intent/)
* [<cite>‘Scope’ in CSS</cite>](http://csswizardry.com/2013/05/scope-in-css/)
* [<cite>Keep your CSS selectors short</cite>](http://csswizardry.com/2012/05/keep-your-css-selectors-short/)
* [<cite>About HTML semantics and front-end architecture</cite>](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/)
* [<cite>Naming UI components in OOCSS</cite>](http://csswizardry.com/2014/03/naming-ui-components-in-oocss/)
* [<cite>Writing efficient CSS selectors</cite>](http://csswizardry.com/2011/09/writing-efficient-css-selectors/)

---

## Spécificité

Comme nous l'avons vu, CSS n'est pas le langage le plus agréable : un namespace global, des fuites un peu partout, d'éventuelles dépendances de lieu, le tout difficile à encapsuler, et basé sur de l'héritage parfois difficile à appréhender… Mais, tout cela n'est rien en comparaison de l'horreur qu'est la spécificité.

Peu importe que votre nommage soit bon, que l'ordre de la source soit impeccable, que la cascade soit parfaitement gérée et que vous ayez correctement écrit vos règles : il suffit d'une règle trop spécifique pour tout briser. C'est un concept qui est susceptible d'ébranler facilement les autres concepts propres à CSS : cascade, héritage et ordre de la source.

Le problème avec la spécificité c'est qu'elle force des choses qui peuvent être très pénible à défaire. Si on prend un véritable exemple dont j'ai été l'auteur il y a quelques années :

    #content table {}

Non seulement ceci est [un sélecteur de piètre intention](#intention) &mdash;je ne voulais pas cibler toutes les `table` de la zone `#content`, je vous une table bien spécifique qui se trouvait là&mdash; c'est un sélecteur bien trop spécifique. Ce fut apparent quelques semaines plus tard, quand j'ai une besoin d'un autre type de `table` :

    #content table {}

    /**
     * Oh-oh! Mes styles sont écrasés par `#content table {}`.
     */
    .my-new-table {}

Le premier sélecteur dépassait largement la spécificité de celui défini *plus bas*, allant donc à l'encontre de l'ordre de la source. Pour corriger le souci, j'avais deux options :

1. refactoriser le CSS et le HTML pour retirer cette ID ;
2. écrire un sélecteur plus spécifique pour l'écraser.

Malheureusement, refactoriser aurait pris trop de temps ; c'était un projet mur et les effets qu'aurait pu engendrer le retrait de cet ID auraient coûté davantage de la seconde option : écrire un sélecteur plus spécifique que le premier.

    #content table {}

    #content .my-new-table {}

Maintenant, on a un sélecteur *encore plus spécifique* que celui que l'on jugeait trop spécifique. Et si on veut pouvoir écraser ces styles, il faudra un sélecteur avec une spécifité égale ou plus grande. C'est l'entrée de la spirale infernale.

La spécificité peut, entre autres :

* limiter la portabilité et réutilisation du code ;
* interrompre et aller à l'encontre de la nature d'héritage de la cascade ;
* causer de la verbosité inutile au sein du projet ;
* empêcher le fonctionnement normal lors d'un changement d'environnement ;
* sérieusement frustrer les développeurs.

Ceci est d'autant plus vrai lorsqu'il s'agit de gros projets avec de nombreux développeurs contribuant au code.

### Toujours la plus basse possible

Le problème avec la spécificité n'est pas tellement qu'elle soit haute ou basse ; c'est le fait qu'elle varie sans pouvoir être amoindrie ou annulée. Le seul moyen de lutter est d'être de plus en plus spécifique &mdash;d'où la notion de <i>specificity war</i> dont on a vu un cas classique plus haut.

Un des conseils plus simples que je puisse vous donner pour vous faciliter la vie quand vous écrivez du code CSS, surtout dans le cas d'un projet d'une taille raisonnable, est de toujours essayer de garder la spécificité la plus petite possible. Assurez-vous qu'il n'y ait pas de grosses variations de spécificité entre les différents sélecteurs du projet, et qu'ils se trouvent tous avec la spécificité la plus basse possible.

En faisant ça, vous vous assurez de ne pas avoir de sélecteurs très spécifiques qui viennent impacter des sélecteurs moins spécifiques ailleurs, ce qui vous aidera grandement dans la maintenance de vos projets, cela va sans dire. Cela signifie aussi que vous réduisez grandement les choses de vous battre avec la notion de spécificité, rendant par la même occasion vos feuilles de styles plus légères.

Voici une liste non-exhaustive des changements que l'on peut faire pour aller dans ce sens :

* ne pas utiliser d'IDs en CSS ;
* ne pas imbriquer les sélecteurs ;
* ne pas qualifier les classes ;
* ne pas chaîner les sélecteurs.

**La spécificité peut être comprise et maîtrisée, mais il est simplement plus sage de l'éviter complètement.**

### Les IDs en CSS

Si l'on souhaite réduire la spécificité de nos sélecteurs de manière générale, il y a une méthode simple et rapide à mettre en place : ne pas utiliser d'IDs en CSS.

Non seulement les IDs ne sont pas réutilisables de par leur nature même, mais elles sont également plus spécifiques que n'importe quel autre sélecteur, ce qui entraîne d'éventuels soucis de spécificité. Quand le reste de vos sélecteurs partage une spécificité relativement basse, les sélecteurs basés sur des IDs sont comparativement extrêmement élevés.

En fait, pour illustrer combien la différence est sévère, voyez comment *1000 classes* chaînées ne peuvent pas surpasser la spécificité d'une simple ID :
[jsfiddle.net/0yb7rque](http://jsfiddle.net/csswizardry/0yb7rque/). <small>(Notez cependant que sur Firefox, vous devriez voir le texte en bleu : c'est un [bug connu](https://twitter.com/codepo8/status/505004085398224896) selon lequel une ID peut être écrasée par 256 classes chaînées.)</small>

<small>**N.B.** Il est bien évidemment tout à fait correct d'utiliser des IDs en HTML et en JavaScript ; c'est uniquement dans le domaine des CSS qu'elles s'avèrent problématiques.</small>

Il est souvent décrié que les développeurs qui choisissent délibérement de ne pas utiliser d'ID en CSS <q>ne comprennent pas comment la spécificité fonctionne</q>. C'est aussi incorrect qu'offensant : peu importe l'expérience, ce comportement ne peut pas être défait, et ce n'est pas un niveau avancé qui va rendre une ID moins spécifique.

Choisir d'abandonner les IDs en CSS, c'est réduire les chances de rencontrer des problèmes de spécificité, surtout dans le cas de gros projets. Tous les efforts devraient être faits afin *d'éviter* d'éventuels soucis. En d'autres termes :

**Ca ne vaut pas le coup.**

### Imbrication

Nous avons déjà vu que l'imbrication des règles les unes dans les autres peut engendrer des dépendances de contexte et par là même du code inefficace, mais il est temps de s'attacher à un autre inconvénient : elle rend les sélecteurs plus spécifiques.

Par imbrication, on ne parle pas nécessairement de l'imbrication des pré-processeurs comme ceci :

    .foo {

        .bar {}

    }

On parle également des sélecteurs descendants ou enfants ; sélecteurs qui se basent sur l'idée d'avoir un élément dans un autre. Cela peut donc concerner n'importe lequel des exemples suivants :

    /**
     * Un élément avec la classe `.bar` dans un élément avec la classe `.foo`.
     */
    .foo .bar {}


    /**
     * Un élément avec la classe `.module-title`
     * directement dans un élément avec la classe `.module`.
     */
    .module > .module-title {}


    /**
     * Un élément `li` dans un élément `ul` dans un élément `nav`.
     */
    nav ul li {}

Que vous obteniez ces sélecteurs via un pré-processeur ou non n'est pas particulièrement important, mais il est bon de noter que **les pré-processeurs vendent cela comme une fonctionnalité, alors qu'il vaut mieux l'éviter autant que faire se peut**.

De manière générale, chaque morceau d'un sélecteur composé ajoute de la spécificité. Par conséquent, moins il y a de parties dans un sélecteur, moins sa spécificité sera haute, or nous ne voulais pas d'une grande spécificité. Pour citer Jonathan Snook :

> …quand vous déclarez vos règles, **utilisez le minimum de sélecteurs possible pour styler un élément.**

Prenons un exemple :

    .widget {
        padding: 10px;
    }

        .widget > .widget__title {
            color: red;
        }

Pour styler un élément avec une classe `.widget__title`, nous avons un sélecteur deux fois plus spécifique qu'il devrait l'être. Cela signifie que si l'on souhaite appliquer des modifications à `.widget__title`, on va avoir besoin d'un autre sélecteur au moins aussi spécifique, si ce n'est plus :

    .widget { ... }

        .widget > .widget__title { ... }

        .widget > .widget__title--sub {
            color: blue;
        }

Non seulement c'est facilement évitable &mdash;on s'est imposé ce problème soi-même&mdash; mais en plus on se retrouve avec un sélecteur deux fois trop spécifique. On a utilisé 200% de la spécificité requise. En plus de *ça*, on introduit de la verbosité inutile dans notre code.

La règle à retenir : **si un sélecteur fonctionne sans être imbriqué, alors on ne l'imbrique pas**.

#### Scope

Un avantage de l'imbrication &mdash;qui malheureusement ne suffit pas à contre-balancer tous les inconvénients d'une sur-spécificité&mdash; est qu'elle confère une sorte de namespace. Un sélecteur comme `.widget .title` encapsule les styles de `.title` dans un contexte `.widget`.

C'est une idée pour fournir à CSS un mécanisme de scope et d'encapsulation, mais ça rend quand même nos sélecteurs deux fois trop spécifiques. Une meilleure approche pour gérer le scope est d'inclure le namespace dans le nommage, ce que l'on fait déjà via le [nommage BEM-like](#notation-bem-like), qui a l'avantage de ne pas accroîte inutilement la spécificité des sélecteurs.

Ainsi nous avons des CSS scopés avec la plus petite spécificité possible ; le must.

##### Pour aller plus loin

* [<cite>‘Scope’ in CSS</cite>](http://csswizardry.com/2013/05/scope-in-css/)

### `!important`

Le terme `!important` provoque des frissons dans le dos de presque tous les développeurs front-end. `!important` est une manifestation directe des problèmes de spécificité ; c'est une sorte de joker dans la guerre des spécificités, qui vient généralement au prix fort. C'est souvent vu comme la technique de la dernière chance &mdash; la tentative désespérée de correction d'énormes problèmes dans le code.

D'ordre général, `!important` est toujours une mauvaise idée mais vous connaissez l'adage :

> Il y a l'exception qui confirme la règle.

Quand on démarre, la règle de <q>ne jamais utiliser `!important`</q> est une bonne règle.

Ceci étant dit, quand on commence à grandir en temps que développeur, on commence à comprendre que l'idée derrière cette règle est simplement de garder une spécificité aussi basse que possible. On apprend alors qu'il y a des cas où les règles sont faites pour être outrepassées.

`!important` a quand même une place dans les projets CSS, mais c'est somme toute rare et doit être fait de manière proactive.

Une utilisation proactive de `!important` signifie que ce soit être utilisé *avant* de se retrouver face à des problèmes de spécificité ; quand on l'utilise comme une garantie et non pas comme un correctif. Par exemple :

    .one-half {
        width: 50% !important;
    }

    .hidden {
        display: none !important;
    }

Ces deux classes *helpers*, ou <i>utilitaires</i>, sont très explicites dans leurs intentions : donner une largeur de moitié à un élément ou le cacher complètement. Si on ne veut pas nécessairement ce comportement, on n'applique pas ces classes. De fait quand on les applique on veut impérativement l'effet escompté.

Ici on utilise `!important` de manière proactive pour s'assurer que ces styles soient toujours effectifs. C'est un usage correct d'`important!` pour garantir un comportement bien particulier, afin qu'il ne soit pas surchargé par quelque chose de plus spécifique.

Une utilisation incorrecte et <i>reactive</i> de `!important` serait de combattre les soucis de spécificités : appliquer `!important` à des déclarations CSS mal conçues. Par exemple, imaginons cette structure HTML :

    <div class="content">
        <h2 class="heading-sub">...</h2>
    </div>

…et ces CSS:

    .content h2 {
        font-size: 2em;
    }

    .heading-sub {
        font-size: 1.5em !important;
    }

Dans ce cas présent, on se rend compte que l'on a utilisé `!important` pour forcer certains styles de `.heading-sub` à écraser ceux de `.content h2`. Ce pourrait être évité de bien des façons, comme utiliser un meilleur sélecteur ou éviter l'imbrication.

Dans ces situations, il est préférable d'investiguer et de refactoriser les règles qui posent problème en réduisant la spécificité générale plutôt que de tomber dans la facilité en surchargeant la spécificité.

**N'utilisez `!important` que de manière proactive, jamais reactive.**

### Contourner les problèmes de spécificité

Avec tout ce que l'on vient de se dire au sujet de la spécificité, comme quoi il faut la garder basse autant que possible, il est de toutes façons inévitable que l'on rencontre des soucis un jour ou l'autre. Peu importe combien on se veut consciencieux, il y aura forcément un moment où on va devoir contourner un souci de spécificité.

Quand cette situation arrive, il est important de trouver une solution aussi fiable et élégante que possible.

Dans le cas où vous devez accroître la spécificité d'une classe, il y a plusieurs options. On peut imbriquer celle-ci dans un autre sélecteur pour augmenter la spécificité. Par exemple, on peut utiliser `.header .site-nav` pour gonfler la spécificité de `.site-nav`.

Le problème avec ça, et on en a déjà parlé, c'est qu'on introduit une dépendance de contexte : ces styles ne fonctionneront que si `.site-nav` se trouvent dans un composant `.header`.

Un hack bien plus fiable qui n'impacte pas la portabilité du composant serait de doubler la classe comme ceci :

    .site-nav.site-nav {}

Ce procédé double la spécificité du sélecteur sans introduire de dépendance d'aucune sorte.

Dans le cas où on a, pour quelque raison que ce soit, une ID dans le markup que l'on ne peut pas remplacer avec une classe, on la cible via un sélecteur d'attribut plutôt qu'un sélecteur d'ID. Par exemple, imaginons que nous avons un widget externe inclus dans notre page. Nous pouvons styler le widget mais pas changer son markup nous-même :

    <div id="third-party-widget">
        ...
    </div>

Nous savons pertinemment que nous ne devons pas utiliser d'ID en CSS mais avons-nous seulement le choix ? Nous devons styler cet élément, sans autre type d'accroche qu'une ID.

On peut faire :

    [id="third-party-widget"] {}

Ici, on cible l'élément en se basant sur un sélecteur d'attribut plutôt qu'une ID, dans la mesure où un sélecteur d'attribut a la même spécificité qu'une classe. Ceci nous permet de styler un élément possédant une ID sans pour autant introduire une haute spécificité.

Gardez à l'esprit que ces astuces *sont* des hacks, qui ne doivent être utilisés qu'en dernier recours.

#### Pour aller plus loin

* [<cite>Hacks for dealing with specificity</cite>](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/)

---

{% include promo-hire.html %}
