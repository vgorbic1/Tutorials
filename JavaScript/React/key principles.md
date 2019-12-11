## Key Principles of React
### Declarative vs. Imperative
Don't touch the DOM. I'll do it. Imerative paradigm is when 
you directly change parts of app in response to user's events) Updating the DOM is one of the biggest performance constrains.
It takes a lot of time. Browser has to repaint (remove and replace) the element and reflow (recalculate the layout) the page 
and move things around. Declarative style (React style) just let React know how the app should look like and React will do 
the rest.
### Componet Architecture
Idea of reusable components. Bigger components contain smaller components like Lego blocks. Components are just JavaScript
classes or functions that receive props and return JSX.
### Uniderectional Data flow
Anytime we want something to change on our web page, React changes the state and updates the DOM accordingly. The data only
flows one way from state to all components. (unlike Angular). It is easier to debug the code.
### UI Libbrary
React only works with user interface. It is a multiplatform concept.
