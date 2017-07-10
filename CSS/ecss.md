## Enduring CSS (ECSS)
Primary goal with ECSS is to isolate styles as opposed to abstracting them.
Depending upon your goals, even at the cost of repetition, isolation can buy you greater
advantages; allowing for predictable styling and simple decoupling of styles.

ECSS approach address the following needs:
- To allow the easy maintenance of a large CSS codebase over time
- To allow portions of CSS code to be removed from the codebase without effecting
the remaining styles
- To make it possible to rapidly iterate on any new designs
- Changing the properties and values that applied to one visual element should not
unintentionally effect others
-Any solution should require minimal tooling and workflow changes to
implement
- Where possible, W3C standards such as ARIA should be used to communicate
state change within the user interface

Structural HTML elements (with the exception of pseudo-elements) are
NEVER referenced in the style sheets as type selectors. In addition ID selectors are
completely avoided in ECSS. Not because ID selectors are bad per se, but because we need a
level playing field of selector strength.

Changes to components are handled via simple overrides. However, the way they are
handled from an authoring perspective makes them easy to manage and reason about.

The term *key selector* is used to describe the right most selector in any CSS
rule. It's the selector you are attempting to affect change on.

ID selectors are infinitely more specific than
class based selectors. This makes overriding any selector containing an ID based selector far
more difficult.

Another practice to avoid when authoring CSS for scale is using type selectors; selectors
that relate to specific markup. For example:
```css
aside#sidebar ul > li a {
  /* Styles */
}
```
We've just unnecessarily tied our rule to specific markup structure.
We want CSS that is as loosely coupled to structure as possible. That way, should we need
to introduce an override (a more specific selector for a particular instance) we can keep
things as vague as possible to get the job done.

### Terminology
- A *module* is the widest, visually identifiable, individual section of functionality
- *Components* are the nested pieces of functionality that are included within a
module
- *Child nodes* are the individual parts that go to make up a component (typically
nodes in the DOM)

### Explanation of selector sections
Let's go back over the various parts of the ECSS selector and the allowed character types:
- Namespace: This is a required part of every selector. The micro-namespace
should be all lowercase/train-case. It is typically an abbreviation to denote context
or originating logic.
- Module or Component: This is a upper camel case/pascal case. It should always
be preceded by a hyphen character `(-)`.
- ChildNode: This is an optional section of the selector. It should be upper camel
case/pascal case and preceded by an underscore `(_)`.
- Variant: This is a further optional section of the selector. It should be written all
lowercase/train-case.

