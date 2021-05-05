---
title: "Intents as CSS"
description: 'Using cascading stylesheets to (pre)define MathML intents'
---


## MathML Intents

MathML Intents is a proposed evolution to be elaborated within MathML4,
a specification that is to be produced by the newly formed 
[Math Working Group of the W3C](https://www.w3.org/Math/)

Intents should help into making loud-readable mathematical formulæ written
in presentation MathML. A rich start of "default intents" has been 
compiled in [this table](https://docs.google.com/spreadsheets/d/e/2PACX-1vTD9H2hQjgXXbkZrqkJQbTawwwrvlDfrTlVZRY8iF49jkJZ2rYfQX4QK39GlLhIuK0Fhhwkm_NnAcqm/pubhtml).
Intents could give a hint toward bringing some _semantic_ into MathML-presentation expressions.


However, it is clear that such a list is never going to be one-size fits all.
Some of main symbols my favorite math topics are not there (e.g. the amalgamated product
of finitely generated groups or the homotopy groups) and different
ways of saying will always come e.g. the pipe when in P(A|B) or in {x| x>3} 
(non-use of a math-specific syntax is intentional ;-)). One plans
an intent attribute value to be puttable on every MathML-presentation
element. That's good and useful for specific intents. But repeating
that the "|"-symbol should be said as a _conditional to_ and not
a _such that_ bloats the source.


---

## What if... 

... the `intent` attribute value could be specified by using a style
of the cascading stylesheet. Let us suppose, for example, that a
`mathintent` property value of CSS exists.

This means that this property can be put inside a rule within the web-page body 
or within a stylesheet and indicate:

- an intent value for every occurrence of a particular MathML-element 
- an intent value for every leaf of a particular cascade of MathML-element (including pseudo-class fun such as first and last)
- an intent value for such but within a particular class

And it also probably means that the best practice where CSS has been applied to accessibility
such as the reading-mode of browsers, the high-contrast skin-change, or user-adjustments can
all be made too.

---

## Examples

### Translating

An author wishes to write down and make effective in his web-publications the 
translations of the intents of his notations. His usage of mathematical symbols
is rather moderate and he holds a table of symbols at the start of his works anyways.

Thus our author realizes a stylesheet for its complete course so that
it is enough to write (with some discipline) presentation and have them speak-aloud-pronounceable.

### Disambiguation through Structure

TODO: P(A|B) vs {x|x>3} because of checking the cascade of `<mo>` by a CSS selector
which checks the exact content of the `mo` elements.

### Scoping by classname

A magazine or conference web-site presents the abstracts of the various contributions.
Some abstracts are from different communities so that, say, the _e_ symbol should either
be pronounced as the Euler or Napier constant. 

Because each abstract can be tagged with a classname denoting the "community" it belongs
to. The different intents are inherited without the editor actually modifying the
MathML expressions.

---

## Challenges & Hopes

Supposing that this becomes widespread practice (indeed, accesibility is becoming
more and more of a legal requirement and intents bring an operational way to do so),
collecting the stylesheets found around the web could offer a way to complement and,
more a challenge, **collect translations** in multiple languages and communities for the
intents' table (the one above really is for the English-speakers only).

Accessibility devices that work with browsers don't get the CSS... That is a problem
if operating on mandate of a browser that has loaded a static HTML page. However, CSS
inheritance works rather well in most browsers and could, thus, be ported to attributes
of the DOM by a JavaScript running in the browser before the accessibility device is addressed?

Changing stylesheet to adjust the purpose might be useful here too: Creating different stylesheets
for different recipients and customising stylesheet because of one's stronger knowledge might
help the users of accessibility devices obtain a more relevant experience. The change could
be in the browser level, at the level of a classroom, at the level of an author, or
even at the software level.

And if CSS is still not the riches selection language... there's a lot of generator
out there... and you can really industrialize the production of the intents to be
applied to the very specific category or a population that needs more and more
relevant mathematical knowledge.

---

## Now what?

This little "what-if musing" was written to enrich the discussion in the Math community and working group.