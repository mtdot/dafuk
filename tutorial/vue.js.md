# Basic

## 6. Re-building the App with Vue
- `v-model` directive
- `v-on:click` or `@click` or `@click.right` directive
- `v-bind:value=` or `:value=` directive
- `v-for` directive
- `v-once` marking element should be evaluate only once, and never be updated again.


- mounting control element by css selector
- `data` property name is fixed, require a function return data object
- `methods` property name is fixed, contains functions definitions
- Vue.js merge all property in data object into global Vue instance so we can access that properties via `this.propertyName` inside methods
```js
data(): { return {}; }
```
or
```js
data: function() { return {}; }
```


```html
<body>
  <div id="app">
    <div>
      <label for="goal">Goal</label>
      <input type="text" id="goal" v-model="enteredValue" />
      <button v-on:click="addGoal">Add Goal</button>
    </div>
    <ul>
      <li v-for="goal in goals">{{ goal }}</li>
    </ul>
  </div>
  <script src="https://unpkg.com/vue@next"></script>
  <script src="app.js"></script>
</body>
```

```js
Vue.createApp({
  data() {
    return {
      goals: [],
      enteredValue: ''
    };
  },
  methods: {
    addGoal() {
      this.goals.push(this.enteredValue);
      this.enteredValue = '';
    }
  }
}).mount('#app');
```

## 14. `Performance` Interpolation and Data Binding
  - Interpolation syntax `{{ varName }}` accept data-binding of a `html tag inner HTML` to property name of Vue's data object.
  - Interpolation syntax `{{ doSomething() }}` for evaluating method: This should be avoid, because `doSomething()` alway be executed when anything on the page changed.
  ```html
  <p>{{ title }}</p>
  ```
  
  - data-binding with a property using `v-bind` directive
  ```html
  <a v-bind:href="pageLink">Goto Page</a>
  ```

## 18. `Security` Outputting Raw HTML Content with v-html
  - Should be avoid to prevent `Cross Site Scripting (XSS) Software Attack` - `Research later`
  ```js
  <p v-html="getSomeHtml()"></p>
  ```
  
## 20. Understanding Event Binding
  - `v-on:<event>`
  - List of events?
  ```js
  <button v-on:click="counter++">Add</button>
  <button v-on:click="counter = counter - 1">Reduce</button>
  <button v-on:click="add(10)">Add 10</button>
  <button v-on:click="setName">Set Name</button> <!-- this will pass event object as default parameter -->
  <button v-on:click="setName($event, 'My Name')">Set Name</button> <!-- passing event object with some parameter -->
  ```
  
## 24. Exploring Event Modifiers
  ```
  <form v-on:submit.prevent="submitForm"> ... </form>
  <button v-on:click.right="...">Click</button>
  <input v-on:keyup.enter="confirmValue"/>
  ```

## 26. Data Binding + Event Binding = Two-Way Binding
  - two bellow attribute is similar, indicating two-way binding
```js
v-model="name"
v-bind:value="name" v-on:input="setName"
```

## 28. `Performance` Introducing Computed Properties
  - `computed` property on Vue's data object
  - pointing to computed method using method name (`fullname`), not including `(` `)` (`fullname()`)
  - almost methods related to renderring contents will be implemented as `computed method`, avoid implement as `normal method`
  - `method` is appropriate for event binding, which need to re-executed on every event trigger

## 29. Working with Watchers
  - `watch` property on Vue's data object
  - `computed` and `watch` methods allow you to react to data changes
  - contains method with same name as properties of Vue's data object
  - methods will be re-executed whenever the property with same name changed
  - useful for some task: reset counter for seconds, timer tasks, send a request when value changed, ...
```js
watch {
  name(newName) {
    this.fullname = newName + " ABCXYZ"
  }
  
  position(newPosition, oldPosition) {
    // do something with both newPosition and oldPosition
  }
}
```

## 33. Adding CSS Classes Dynamically
  - class will be add to element if value of the key is evaluated as `true`
  - classes can be combined with fixed classes and dynamic classes
  - dynamic classes can be implemented via `computed` methods, but only useful with complex logic to fill classes
```js
<div :class="{active: isActive}">...</div>
<div class="demo" :class="{active: isActive}">...</div>
<div class="demo" :class="boxAClasses">...</div> <!-- boxAClasses is a computed method -->
```
## 40. Rendering Content Conditionally
  - `<p v-if="items.length === 0">Items non-empty</p>`
  - `v-else` have to be used by the element directly after the element has `v-if`
  - `v-show` work same as `v-if` but work standalone (show element if the condition matched). The different is `v-show` using `display: none` to control visibility (Including in DOM) but `v-if` completely remove element in DOM if condition not matched. Only use `v-show` for case element need to toggle frequently.
  - `v-for="(item, index) in items"` for loop with index
  - `v-for="(value, key, index) in {name: 'Foo', age: 20}" for loop through object keys & index
  - `v-for="num in 10"` loop for range [1, 10]
  - remove element by index: [1,2,3,4].splice(2, 1) // remove from index 2 form 1 elements

## 46. Lists & Keys
  - `@click.stop`: stop propogation click event from children element to parent element. Using this prevent handling click event on both children and parent.
  - Vue's removing element mechanism in DOM have a potential issue of losing content in case that element have no `v-bind:key` property (`:key`)
  - avoid using `index` of element as `key` to prevent the issue related to `index` change every adding/removing item from list

## 60. Vue Reactivity: A Deep Dive
  - understanding `Proxy` object to obtain changes on js objects.

## 62. Understanding Templates
  - understand `template` property of when creating Vue instance

## 63. Working with Refs
  - `ref` keyword: `<input type="text" ref="userInput"/>
  - access ref via `$refs`: `this.refs.userInput`

## 65. Vue App Lifecycle - Theory
  - [Lifecycle](https://samsungu.udemy.com/course/vuejs-2-the-complete-guide/learn/lecture/21463392#overview)
  - All callback belong to Vue Instance
 
## 85. Adding Styling
  - add style for component inside `<style>` tag
