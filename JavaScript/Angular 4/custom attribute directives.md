## Custom Attribute Directives

To create a directive with CLI:
```
ng g d directivename
```
- g - generate
- d - directive

You may want to put all your directives in one directroy called `directives`

### Basic Attribute Directive
basic-highlight.directive.ts
```javascript
import { Directive, ElementRef, OnInit } from '@angular/core';

@Directive({
    selector: '[appBasicHighlight]' // put in square brackets to easily use it in the template
})
export class BasicHighlightDirective implements OnInit {
    constructor(private elementRef: ElementRef) {      
    }

    ngOnInit() {
        this.elementRef.nativeElement.style.backgroundColor = "green";
    }
}
```
Do not forget to register the directive in `app.module.ts`

app.component.html
```html
<p appBasicHighlight>Style me with basic directive!</p>
```

### Beter Approach to Set Attribute Directive (with Renderer2)
You should use the Renderer for any DOM manipulations:

better-highlight.directive.ts
```javascript
import { Directive, Renderer2, OnInit, ElementRef } from '@angular/core';

@Directive({
  selector: '[appBetterHighlight]'
})
export class BetterHighlightDirective implements OnInit {

  constructor(private elRef: ElementRef, private renderer: Renderer2) { }

  ngOnInit() {
    this.renderer.setStyle(this.elRef.nativeElement, 'background-color', 'blue');
  }

}
```
app.component.html
```html
<p appBetterHighlight>Style me with basic directive!</p>
```
### HostListener Decorator for Dynamic Rendering of Attribute Directive
Use `HostListener` to and some dynamic rendering:

better-highlight.directive.ts
```javascript
import { Directive, Renderer2, OnInit, ElementRef, HostListener } from '@angular/core';

@Directive({
  selector: '[appBetterHighlight]'
})
export class BetterHighlightDirective implements OnInit {

  constructor(private elRef: ElementRef, private renderer: Renderer2) { }

  ngOnInit() {
    //this.renderer.setStyle(this.elRef.nativeElement, 'background-color', 'blue');
  }

  @HostListener('mouseenter') mouseover(eventData: Event) {
    this.renderer.setStyle(this.elRef.nativeElement, 'background-color', 'blue');
  }

  @HostListener('mouseleave') mouseleave(eventData: Event) {
    this.renderer.setStyle(this.elRef.nativeElement, 'background-color', 'transparent');
  }

}
```
app.component.html
```html
<p appBetterHighlight>Style me with basic directive!</p>
```

