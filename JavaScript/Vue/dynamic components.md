## Dynamic Components
Dynamic components allow for dynamic replacement of part of the template with those components' templates. Use reserved tag 
`<component>` for it:
```
// App.vue
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12">
            <button @click="selectedComponent = 'appQuote'">Quote</button>
            <button @click="selectedComponent = 'appAuthor'">Author</button>
            <button @click="selectedComponent = 'appNew'">New</button>
               <component :is="selectedComponent">
                   <p>Default Content</p>
               </component>
            </div>
        </div>
    </div>
</template>

<script>
    import Quote from './components/Quote.vue'
    import Author from './components/Author.vue'
    import New from './components/New.vue'  

    export default {
        data: function() {
            return {
                selectedComponent: 'appQuote'
            }
        },
        components: {
            appQuote: Quote,
            appAuthor: Author,
            appNew: New
        }
    }
</script>

<style>
</style>
```
```
// Author.vue (similar content in Quote.vue and New.vue)
<template>
    <div>
        <h3>The Author</h3>
    </div>
</template>

<script>
</script>

<style>
</style>
```
