<script src="https://unpkg.com/vue"></script>

# Transitions in Vue.js 


## Talk Animating VueJS

As superfluous as something like animation may initially seem, **you can tell a lot about framework by the way that it handles the concept of time**. 

Idiosyncrasies and race conditions in rendering reveal themselves, pauses in DOM and virtual DOM diffing can be exposed. 

This is one of the ways Vue shows itself to be uniquely capable and elegant.

In this session, we'll cover the basics of working with Vue, how to use the component and some of its offerings to create fluid effects in the browser. 

We'll move on to 

* watchers, 
* the reactivity system, and 
* transitioning state. 

Finally, we'll talk about 

* lifecycle methods, 
* SVG, and 
* pushing our animations to the next level.

### EVENT:

SmashConf Barcelona 2017 (https://www.smashingmagazine.com/)

### SPEAKER: 

Sarah Drasner

* [YouTube Video](https://youtu.be/Vp37fWKOlV4)

## Vue Guide: Enter/Leave and List Transitions 

* [Enter/Leave & List Transitions](https://vuejs.org/v2/guide/transitions.html)

### Example

```html
<div id="demo">
  <button v-on:click="show = !show">
    Toggle
  </button>
  <transition name="fade">
    <p v-if="show">hello</p>
  </transition>
</div>

<script>
    new Vue({
      el: '#demo',
      data: {
        show: true
      }
    })
</script>

<style>
    .fade-enter-active, .fade-leave-active {
      transition: opacity .5s;
    }
    .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
      opacity: 0;
    }
</style>
``` 

[See the example running](https://crguezl.github.io/animating-vuejs/hello-transition.html)

### The Transition Component Algorithm

When an element wrapped in a **transition component** is inserted or removed, this is what happens:

1. Vue will automatically sniff whether the target element has CSS transitions or animations applied. 
2. If it does, CSS transition classes will be added/removed at appropriate timings.
3. If the transition component provided JavaScript hooks, these hooks will be called at appropriate timings.
4. If no CSS transitions/animations are detected and no [JavaScript hooks](https://vuejs.org/v2/guide/transitions.html#JavaScript-Hooks) are provided, 
   * the DOM operations for insertion and/or removal will be executed immediately on next frame 
   * (Note: this is a browser animation frame, different from Vue’s concept of `nextTick`).


### Transition Classes

There are six classes applied for enter/leave transitions.

* `v-enter`: Starting state for enter. 
  * Added before element is inserted, removed one frame after element is inserted.
* `v-enter-active`: Active state for enter. 
  * Applied during the entire entering phase. 
  * Added before element is inserted, removed when transition/animation finishes. 
  * This class can be used to define the duration, delay and easing curve for the entering transition.
* `v-enter-to`: Only available in versions 2.1.8+. Ending state for enter. 
  * Added one frame after element is inserted (at the same time `v-enter` is removed), removed when transition/animation finishes.
* `v-leave`: Starting state for leave. 
  * Added immediately when a leaving transition is triggered, removed after one frame.
* `v-leave-active`: Active state for leave. 
  * Applied during the entire leaving phase. 
  * Added immediately when leave transition is triggered, removed when the transition/animation finishes. 
  * This class can be used to define the duration, delay and easing curve for the leaving transition.
* `v-leave-to`: Only available in versions 2.1.8+. Ending state for leave. 
  * Added one frame after a leaving transition is triggered (at the same time v-leave is removed), removed when the transition/animation finishes.