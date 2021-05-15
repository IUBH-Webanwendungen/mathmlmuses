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

... the `intent` attribute value could be specified by using styles
of the cascading stylesheet. Let us suppose, for example, that a
`mathintent-<intent-pattern>` property value of CSS exists for each
thinkable intent-pattern (that's the _known notation_ in
[the intent values table](https://docs.google.com/spreadsheets/d/e/2PACX-1vTD9H2hQjgXXbkZrqkJQbTawwwrvlDfrTlVZRY8iF49jkJZ2rYfQX4QK39GlLhIuK0Fhhwkm_NnAcqm/pubhtml)).


This means that this property can be put inside a rule within the web-page body 
or within a stylesheet and indicate:

- an intent value for every occurrence of a particular MathML-element's pattern (as is done in the list) 
- an intent value for such but within a particular class (e.g. an indication that a given expression is in probability-theory,
  e.g. <nobr>P(A|B)</nobr> or that other is a set description as in <nobr>{x | x² > 1}</nobr>.

And it also probably means that the best practice where CSS has been applied to accessibility
such as the reading-mode of browsers, the high-contrast skin-change, or user-adjustments can
all be made too.

---

## Examples

### Translating

An author wishes to write down and make effective in his web-publications in, say, German.
For this, he wishes to apply translations of the intents for his notations. His usage of mathematical symbols
is rather moderate and he holds a table of symbols at the introduction of his web-publications anyways.

Thus our author realizes a stylesheet for its his web-publication so that
it is enough to write presentation MathML and have them speak-aloud-pronounceable in German.

A slight extract could be the following, where the suffix after ``mathintent`` should be read as
a pattern of MathML element names and character names either as entity or unicode names.

```css
  *[lang="de"] {
      mathintent-mo-equal: "$1 gleich $2";
      mathintent-mo-lt:    "$1 kleiner als $2";
      mathintent-mi-cm:    "Zentimeter";
  }
```

### Mark context to choose intent

While the list of intents provides an intent for many symbol patterns, there may be a lot of ambiguity left.
As an example ``<mo>|</mo>`` could be automatically endowed with:

- the intent ``such-that`` with a speech hint ``$1 such that $2``
- the intent ``conditional-probability`` with a speech hint ``$1 given $2``

Supposing that the following stylesheet can be written: 
```css
  .conditional-prob {
    mathintent-mo-mid: "$1 given $2";
  }
  .set {
    mathintent-mo-mid: "$1 given $2";
  }
```
Note that `mid` is the name of the entity
of the pipe character, it could have been `DIVIDES` (the unicode name), `VerticalBar` or...
The above stylesheet could then be used in the following expressions:
 

```xml
<math>
  <mrow class="conditional-prob">
    <mo>P</mo>
    <mo>(</mo>
    <mi>A</mi>
    <mo>|</mo>
    <mi>B</mi>
    <mo>)</mo>
  </mrow>
  <mo>=</mo>
  <mrow class="set">
    <mo>P</mo>
    <mo>(</mo>
    <mfenced open="{" close="}">
      <mrow>
        <mi>x</mi>
        <mo>|</mo>
        <msup>
          <mi>x</mi>
          <mn>2</mn>
        </msup>
        <mo>&gt;</mo>
        <mn>1</mn>
      </mrow>
    </mfenced>
  </mrow>
</math>
```


### Scoping by classname

A magazine or conference web-site presents the abstracts of the various contributions.
Some abstracts are from different communities so that, say, the expression _A~B_ should either
be pronounced as _A is congruent to B_ or as _A follows the distribution B_. 

Because each abstract can be tagged with a classname denoting the "area" it belongs
to. The different intents are inherited without the editor actually modifying the
MathML expressions of each of the abstracts.

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

And if CSS is still not the right selection language for the stylesheets to be authored... 
there's a lot of generator  out there: You can really industrialize the production of the CSS rules
that will produce intents to be  applied to the very specific category or media.

---

## Now what?

This little "what-if musing" was written to enrich the discussion in the Math community and working group.
After a first [announce](https://lists.w3.org/Archives/Public/public-mathml4/2021May/0001.html), 
David Farmer and Deyan Ginev commented which resulted to the introduction of a property prefix.