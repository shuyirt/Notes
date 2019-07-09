## HTMl Selector 

```html
<p> What color do you like? </p>

p {
	color: red
}
```

## class Selector

```
<li class="first">Create an HTML document</li>

.first {
  font-weight: bold;
}
```

## ID selector

```
<p id="polite"> — "Good morning."</p>

#polite {
  font-family: cursive;
}
```

## Universal Selector

The universal selector (`*`) is the ultimate joker. It allows selecting all elements on a page. As it is rarely used to apply a style to every element on a page, it is often used in combination with other selectors (see [Combinators](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Combinators_and_multiple_selectors).)

```
* {
  padding: 5px;
  border: 1px solid black;
  background: rgba(255,0,0,0.25)
}
```

## Presence and value attribute selectors

```html
  <li data-quantity="1kg" data-vegetable>Tomatoes</li>
  /* All elements with the attribute "data-vegetable"
     are given green text */
  [data-vegetable] {
    color: green;
  }

  <li data-quantity="optional 10ml" data-vegetable="liquid">Olive oil</li>
  /* All elements with the attribute "data-vegetable"
     with the exact value "liquid" are given a golden
     background color */
	[data-vegetable="liquid"] {
    background-color: goldenrod;
  }
  

  <li data-quantity="700g" data-vegetable="not spicy like chili">Red pepper</li>
  /* All elements with the attribute "data-vegetable",
     containing the value "spicy", even among others,
     are given a red text color */
  [data-vegetable~="spicy"] {
    color: red;
  }
  
```

## ubstring value attribute selectors

Attribute selectors in this class are also known as "RegExp-like selectors", because they offer flexible matching in a similar fashion to [regular expression](https://developer.mozilla.org/en-US/docs/Glossary/regular_expression) (but to be clear, these selectors are not true regular expression):

- `[attr]`
  - Represents elements with an attribute name of *attr*.

- `[attr=value]`
  - Represents elements with an attribute name of *attr* whose value is exactly *value*.
- `[attr~=value]`
  - Represents elements with an attribute name of *attr* whose value is a whitespace-separated list of words, one of which is exactly *value*.
- `[attr|=value]`
  - Represents elements with an attribute name of *attr* whose value can be exactly *value* or can begin with *value* immediately followed by a hyphen, `-` (U+002D). It is often used for language subcode matches.
- `[attr^=value]`
  - Represents elements with an attribute name of *attr* whose value is prefixed (preceded) by *value*.
-  `[attr$=value]`
  - Represents elements with an attribute name of *attr* whose value is suffixed (followed) by *value*.
- `[attr*=value]`
  - Represents elements with an attribute name of *attr* whose value contains at least one occurrence of *value* within the string.
- `[attr operator value i]`
  - Adding an `i` (or `I`) before the closing bracket causes the value to be compared case-insensitively (for characters within the ASCII range).
- `[attr operator value s]
  - Adding an `s` (or `S`) before the closing bracket causes the value to be compared case-sensitively (for characters within the ASCII range).

```css
/* Classic usage for language selection */
[lang|="fr"] {
  font-weight: bold;
}

/* All elements with the attribute "data-quantity", for which
   the value starts with "optional" */
[data-quantity^="optional"] {
  opacity: 0.5;
}

/* All elements with the attribute "data-quantity", for which
   the value ends with "kg" */
[data-quantity$="kg"] {
  font-weight: bold;
}

/* All elements with the attribute "data-vegetable" containing
   the substring "not spicy" are turned back to green */
[data-vegetable*="not spicy"] {
  color: green;
}
```

## Pseudo-class

- [`:active`](https://developer.mozilla.org/en-US/docs/Web/CSS/:active)
- [`:checked`](https://developer.mozilla.org/en-US/docs/Web/CSS/:checked)
- [`:default`](https://developer.mozilla.org/en-US/docs/Web/CSS/:default)
- [`:dir`](https://developer.mozilla.org/en-US/docs/Web/CSS/:dir)
- [`:disabled`](https://developer.mozilla.org/en-US/docs/Web/CSS/:disabled)
- [`:empty`](https://developer.mozilla.org/en-US/docs/Web/CSS/:empty)
- [`:enabled`](https://developer.mozilla.org/en-US/docs/Web/CSS/:enabled)
- [`:first`](https://developer.mozilla.org/en-US/docs/Web/CSS/:first)
- [`:first-child`](https://developer.mozilla.org/en-US/docs/Web/CSS/:first-child)
- [`:first-of-type`](https://developer.mozilla.org/en-US/docs/Web/CSS/:first-of-type)
- [`:fullscreen`](https://developer.mozilla.org/en-US/docs/Web/CSS/:fullscreen)
- [`:focus`](https://developer.mozilla.org/en-US/docs/Web/CSS/:focus)
- [`:focus-within`](https://developer.mozilla.org/en-US/docs/Web/CSS/:focus-within)
- [`:hover`](https://developer.mozilla.org/en-US/docs/Web/CSS/:hover)
- [`:indeterminate`](https://developer.mozilla.org/en-US/docs/Web/CSS/:indeterminate)
- [`:in-range`](https://developer.mozilla.org/en-US/docs/Web/CSS/:in-range)
- [`:invalid`](https://developer.mozilla.org/en-US/docs/Web/CSS/:invalid)
- [`:lang`](https://developer.mozilla.org/en-US/docs/Web/CSS/:lang)
- [`:last-child`](https://developer.mozilla.org/en-US/docs/Web/CSS/:last-child)
- [`:last-of-type`](https://developer.mozilla.org/en-US/docs/Web/CSS/:last-of-type)
- [`:left`](https://developer.mozilla.org/en-US/docs/Web/CSS/:left)
- [`:link`](https://developer.mozilla.org/en-US/docs/Web/CSS/:link)
- [`:matches()`](https://developer.mozilla.org/en-US/docs/Web/CSS/:matches)
- [`:not`](https://developer.mozilla.org/en-US/docs/Web/CSS/:not)
- [`:nth-child`](https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-child)
- [`:nth-last-child`](https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-last-child)
- [`:nth-last-of-type`](https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-last-of-type)
- [`:nth-of-type`](https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-of-type)
- [`:only-child`](https://developer.mozilla.org/en-US/docs/Web/CSS/:only-child)
- [`:only-of-type`](https://developer.mozilla.org/en-US/docs/Web/CSS/:only-of-type)
- [`:optional`](https://developer.mozilla.org/en-US/docs/Web/CSS/:optional)
- [`:out-of-range`](https://developer.mozilla.org/en-US/docs/Web/CSS/:out-of-range)
- [`:read-only`](https://developer.mozilla.org/en-US/docs/Web/CSS/:read-only)
- [`:read-write`](https://developer.mozilla.org/en-US/docs/Web/CSS/:read-write)
- [`:required`](https://developer.mozilla.org/en-US/docs/Web/CSS/:required)
- [`:right`](https://developer.mozilla.org/en-US/docs/Web/CSS/:right)
- [`:root`](https://developer.mozilla.org/en-US/docs/Web/CSS/:root)
- [`:scope`](https://developer.mozilla.org/en-US/docs/Web/CSS/:scope)
- [`:target`](https://developer.mozilla.org/en-US/docs/Web/CSS/:target)
- [`:valid`](https://developer.mozilla.org/en-US/docs/Web/CSS/:valid)
- [`:visited`](https://developer.mozilla.org/en-US/docs/Web/CSS/:visited)

## pseudo-element

- [`::after`](https://developer.mozilla.org/en-US/docs/Web/CSS/::after)
- [`::before`](https://developer.mozilla.org/en-US/docs/Web/CSS/::before)
- [`::first-letter`](https://developer.mozilla.org/en-US/docs/Web/CSS/::first-letter)
- [`::first-line`](https://developer.mozilla.org/en-US/docs/Web/CSS/::first-line)
- [`::selection`](https://developer.mozilla.org/en-US/docs/Web/CSS/::selection)
- [`::backdrop`](https://developer.mozilla.org/en-US/docs/Web/CSS/::backdrop)

## Combinators

| Name                                                         | Syntax  | Selects                                                      |
| :----------------------------------------------------------- | :------ | :----------------------------------------------------------- |
| Selector list                                                | `A, B`  | Any element matching A and/or B (see [Groups of selectors on one rule](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Combinators_and_multiple_selectors#Groups_of_selectors_on_one_rule), below - **Group of Selectors** is not considered to be a combinator). |
| [Descendant combinator](https://developer.mozilla.org/en-US/docs/Web/CSS/Descendant_selectors) | `A B`   | Any element matching B that is a *descendant* of an element matching A (that is, a child, or a child of a child, etc.). the combinator is one or more spaces or dual greater than signs. |
| [Child combinator](https://developer.mozilla.org/en-US/docs/Web/CSS/Child_selectors) | `A > B` | Any element matching B that is a *direct child* of an element matching A. |
| [Adjacent sibling combinator](https://developer.mozilla.org/en-US/docs/Web/CSS/Adjacent_sibling_selectors) | `A + B` | Any element matching B that is the next *sibling* of an element matching A (that is, the next child of the same parent). |
| [General sibling combinator](https://developer.mozilla.org/en-US/docs/Web/CSS/General_sibling_selectors) | `A ~ B` | Any element matching B that is one of the next *siblings* of an element matching A (that is, one of the next children of the same parent). |

[https://www.w3schools.com/cssref/css_selectors.asp](https://www.w3schools.com/cssref/css_selectors.asp)

https://css-tricks.com/specifics-on-css-specificity/