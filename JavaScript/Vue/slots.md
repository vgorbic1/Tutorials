## Slots
The slots allow to pass code rendered outside to the child component:
```
// Parent component
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12">
               <app-quote>
                    <h1>A wonderful {{ quote }}!</h1>
               </app-quote>
            </div>
        </div>
    </div>
</template>

<script>
    import Quote from './components/Quote.vue'
    export default {
        data: function() {
            return {
                quote: 'place';
            }
        }
        components: {
            appQuote: Quote
        }
    }
</script>

<style>
</style>
```
```
// Child Component
<template>
    <div>
        <slot></slot>
    </div>
</template>

<script>
export default {
    props: ['quote']
}
</script>

<style scoped>
    div {
        border: 1px solid #ccc;
        box-shadow: 1px 1px 2px black;
        padding: 30px;
        margin: 30px auto;
        text-align: center;
    }
</style>
```
The style of the child will apply to the "slotted" code.

### Named Slots
To split the data, use named slots:
```
// Parent component
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12">
               <app-quote>
                    <h1 slot="title">The Title</h1>
                    <p slot="content">The Content</p>
               </app-quote>
            </div>
        </div>
    </div>
</template>
...
```
```
// Child Component
<template>
    <div>
        <div class="title">
            <slot name="title"></slot>
        </div>
         <div class="content">
            <slot name="content"></slot>
        </div>
    </div>
</template>
...
```

### Mixed Slots
You may have a mix of named and unnamed slots. In this case everything that is passing in and has unndamed slot will be rendered
in a default (empty) slot: `<slot></slot>`. 

You can put content inside the `<slot></slot>`. This content will be shown if no such slot is assigned in the parent component:
```
// Parent Component
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12">
               <app-quote>
                    <h1 slot="title">The Title</h1>
               </app-quote>
            </div>
        </div>
    </div>
</template>
...
```
```
// Child Component
<template>
    <div>
        <div class="title">
            <slot name="title"></slot>
        </div>
         <div class="content">
            <slot name="content">Something</slot>
        </div>
    </div>
</template>
...
```
