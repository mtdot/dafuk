# Basic

## 6. Re-building the App with Vue
- `v-model` directive
- `v-on:click` directive
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
