## Transition
You can animate any (but only one) element of the DOM that is inside `transition` tags.
You van use both `v-if` or `v-show` directives.

### Fade Effect
Use transition property with `.fade-` CSS class:
```
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
You can bind the `name=""` dynamically:
```
<transition :name="alertAnimation">
...
```
### Slide Effect
Use animation property with `.slide-` CSS class
```
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
### Mixing Effects
Combine transition and animation properties. If you mix both make sure to mention which type dictates the time length with
having either `type="animation"` or `type="transition"`.
```
<template>
...
<button @click="show = !show">Show Alert</button>
<transition name="slide" type="animation">
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
    opacity: 0;
  }
  .slide-enter-active {
    animation: slide-in 1s ease-out forwards;
    transition: opacity .5s;
  }
  .slide-leave {
  }
  .fade-leave-active {
    animation: slide-out 1s ease-out forward;
    transition: opacity 1s;
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
### Animate upon Page Loaded
To start animaion when the page is loaded use `appear` property:
```
...
<transition name="fade" appear>
...
```
### Custom Animation Classes
If you need further finetune your animations use third-party animation libraries, for examle [Animate.css](https://github.com/daneden/animate.css/). With it in the themplate you may specify what custom CSS classes you want to use.
```
<transition
  eneter-active-class="animated bounce"
  leave-active-class="animated shake"
> ...
```
### Switch Between Two Elements
- `out-in` animate the first element and then the second.
- `in-out` animate the second element and then the first.

Make sure that the `key=""` properties are added to each element: 
```
<template>
...
<transition name="alertAnimation" mode="out-in">
  <p v-if="show" key="info">Some Alert Here</p>
  <p v-else key="warning">Some Warning Here</p>
</transition>
...
</template>
```
### Transition Hooks
![th](https://github.com/vgorbic1/Tutorials/blob/master/JavaScript/Vue/images/th.jpg)
Use methods attached to the transition hooks to execure JavaScript animations. If you
do not use any CSS transitions (animations), make sure
you have `:css="false"` to make Vue.js skip the phase of looking at the `<style>`.
```
<button @click="load = !load">Load</button>
<transition
  @before-enter="beforeEnter"
  @enter="enter"
  @after-enter="afterEnter"
  @enter-cancelled="enterCancelled"
  @before-leave="beforeLeave"
  @leave="leave"
  @after-leave="afterLeave"
  @leave-cancelled="leaveCancelled"
  :css="false"
>
  <div style="width; 100px; height: 300px; background-color: green; v-if="load">TEXT</div>
</transition>
<script>
...
  data() {
    return {
      load: true,
      elementWidth: 100
    },
    methods: {
      beforeEnter(el) {
        this.elementWidth = 100;
        el.style.width = this.elementWidth + 'px';
      },
      enter(el, done) {
        // grow the width
        let round = 1;
        const interval = setInterval(() => {
          el.style.width = (this.elementWidth + round * 10) + 'px';
          round++;
          if (round > 20) {
            clearInterval(interval);
            done();
          }
        }, 20);
      },
      afterEnter(el) {
      },
      enterCancelled(el) {
      },
      beforeLeave() {
        this.elementWidth = 300;
        el.style.width = this.elementWidth + '300px';
      },
      leave(el, done) {
        // decrease the width
        let round = 1;
        const interval = setInterval(() => {
          el.style.width = (this.elementWidth - round * 10) + 'px';
          round++;
          if (round > 20) {
            clearInterval(interval);
            done();
          }
        }, 20);
      },
      afterLeave(el) {
      },
      leaveCancelled(el) {
      }
    }
  ...
  ```
