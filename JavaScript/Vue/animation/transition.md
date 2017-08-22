## Transition
You can animate any (but only one) element of the DOM that is inside `transition` tags:

### Fade Effect
Transition with `.fade-` CSS class:
```javascript
<template>
...
<button @click="show = !show">Show Alert</button>
<transition name="fade">
  <p v-if="show">Some Alert Here</p>
</transition>
...
</template>

<secript>
...
  data() {
    return {
      show: false
    }
  }
...
</script>

<style>
  .fade-enter {
    opacity: 0;
  }
  .fade-enter-active {
    transition: opacity 1s;
  }
  .fade-leave {
  }
  .fade-leave-active {
    transition: opacity 1s;
    opacity: 0;
  }
</style>
```
Animation with `.slide-` CSS class
```javascript
<template>
...
<button @click="show = !show">Show Alert</button>
<transition name="slide">
  <p v-if="show">Some Alert Here</p>
</transition>
...
</template>

<secript>
...
  data() {
    return {
      show: false
    }
  }
...
</script>

<style>
  .slide-enter {
  }
  .slide-enter-active {
    animation: slide-in 1s ease-out forwards;
  }
  .slide-leave {
  }
  .fade-leave-active {
    animation: slide-out 1s ease-out forward;
  }
  @keyframes slide-in {
    from {
      transform: translateY(20px);
    }
    to {
      transform: translateY(0);
    }
  }
    @keyframes slide-out {
    from {
      transform: translateY(0);
    }
    to {
      transform: translateY(20px);
    }
  }
</style>
```
