## ECSS
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

