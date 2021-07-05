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

## 84. Adding a Component
  - define component
  - `template` area
  - `script` area
  - add style for component inside `<style>` area
  - 
  ```js
  <template>
    <h1>{{name}}</h1>
  </template>
  <script>
  export default {
    data() {
      return {
        name: "Abcxyz"
      }
    }
    methods: {
      // same as app
    }
  }
  </script>
  ```
  - registerring component
  ```
  app = createApp(App);
  app.component('friend-contact', FriendContact);
  ```
  
## 89. Introducing "Props" (Parent => Child Communication)
  - `props` define all available property name
  - `props` by object
  - validating props
  
  ```
  export default {
    //props: [
    //  "name", // => name, this.name
    //  "phoneNumber", // => phone-number, this.phoneNumber
    //  "emailAddress" // => email-address, this.emailAddress
    //]
    
    props: {
      name: {
        type: String,
        required: true
      },
      phoneNumber: String,
      emailAddress: String,
      isFavorite: {
        type: String,
        required: false,
        default: "0",
        validator: function(value) {
          return value === '0' || value === '1';
        }
      }
    }
  }
  ```
  
## 90. Prop Behavior & Changing Props
  - `prop` cannot be changed by component it self, and can only changed by parent component.
  - instead, create a `internal data property` and initialize it with value of `prop`, then you can update it internaly

## 94. Emitting Custom Events (Child => Parent Communication)
  - `$emit('event-name')` from child component
  - `$emit('event-name', this.id)` from child component to pass parameter
  - `@event-name="<method>"` on parent component

## 95. Defining & Validating Custom Events
  ```
    export default {
    
      props: {
        // ...
      }

      // emits: ['toogle-item'] // defining without validating
      emits: { // defining with validating
        'toogle-item': function(id) { // defining
          // validating
          if (id) {
            return true;
          } else {
            return false;
          }
        }
      }
    }
  ```
  
  ## 96. Prop / Event Fallthrough & Binding All Props
  - `Prop / Event Fallthrough`: Props and events added on a custom component tag automatically fall through to the root component in the template of that component. You can get access to these fallthrough props on a built-in `$attrs` property (e.g. `this.$attrs`)
  - `Binding All Props`: With `v-bind="person"` you pass all key-value pairs inside of `person` as `props` to the component
    
## 99. A Potential Problem
  - `Prop / Event Fallthrough` might be unuseful when you have to pass prop/event via multiple layer of component: com1 > com2 > com3 > com4
    
## 100. Provide + Inject To The Rescue
  - `provide` NOT WORK incase that assigning property to a new one (`this.arrayProperty = this.arrayProperty.filter(...)`) so, instead, try to modify the property.
  - `provide` property of data object in `script` section of parent component
  ```
  <script>
  export default {
    // provide object directly
    //provide: {
    //  topics: {
    //    {...},
    //    {...}
    //  }
    //}
    
    // provide component property
    data() {
      return {
        topics: {
          // ...
        ]
      }
    },
    
    methods: {
      activateTopic(topicId) {
        // ...
      }
    }
    
    provide() {
      return {
        topics: this.topics             // provide value
        selectTopic: this.activateTopic // provide callback
      }
    }
  }
  </script>
  ```
  - `inject` property inside any child component
  ```
  <script>
  export default {
    inject: ['topics', 'selectTopic']
  }
  </script>
  ```

## 107. Global vs Local Components
  - register all component as global is not good.
  - register component locally

## 108. Scoped Styles
```
<style scoped>
...
</style>
```

## 109. Introducing Slots
  - same as ReactJS `props.children`: `<slot></slot>`
  - named slot: using `<slot name="abc"></slot>` for implement multiple `slot` on component. Setup template for named slot (on the place that using component): `<template v-slot:abc>...</template>` or `<template #abc>...</template>`
  - `<style>` not affect on `template` element, all `style` for `slot` should be put on component contains `slot` tag
  - default content for `slot`
  - check if named slot exist
  ```
  <header v-if="$slots.header">
    <slot name="header>
    ...
    </slot>
  </header>
  ```
  - Scoped slot: passing data from component defining `slot` (containing `slot`) to component that using the `slot` (component passing markup to `slot`
  ```
  // component define slot
  <slot v-bind:item="goal"></slot>
  // or short-hand
  <slot :item="goal" another-prop="..."></slot>
  
  // the component that passing markup to slot
  <course-goals>
    <template #default="slotProps"> // 'slotProps' contains all properties of slot above
      <h2>{{ slotProps.item }}</h2>
      <p>{{ slotProps['another-prop'] }}</p> // props name NOT automatically convert to 'anotherProp'
    </template>
  </course-goals>
  ```
  - For single slot, using this short-hand
  ```
  <course-goals #default="slotProps">
    ...
  </course-goals>
  ```
  
  ## 114. Dynamic Components
  - `<component></component>` tag
    ```
    <component v-bind:is="selectedComponent"></component> // bind component name as 'selectedComponent' property
    <component :is="selectedComponent"></component> // short-hand
    ```
  - using `<keep-alive></keep-alive>` for making dynamic component alive when switching component

## 117. Teleporting Elements
  - same as portal feature of ReactJS
  - `<teleport></teleport>` tag
  ```
  <teleport to="body"> // teleport by css selector
    ...
  </template>
  ```
  
## 118. Working with Fragments
  - multiple root element is ok on VueJS v3 thanks to Fragments feature (Not work on VueJS v2)
  
## 120. Moving to a Different Folder Structure
  - Better project structure
  
## 139. Working with v-model Modifiers and Numbers
  - `v-model.trim`: trim text before passing to property
  - `v-model.numer`: convert to number before passing to property

## 141. Using v-model with Checkboxes & Radiobuttons
  - Common: need to set same `v-model:property` to all checkbox & radiobutton on group
  - Common: need to set different `value="value_name"` to each available value on Checkbox & RadioButton group
  - `checkbox`: property contains checkbox data should be array
  - SINGLE `checkbox`: property can be `true`/`false` and without `value` property on checkbox HTML tag.
  - using `@blur` built-in event to validate data on lost focus, combining with binding class `:class="{invalid: inputValid === 'invalid'}"`

## 144. Using v-model on Custom Components
  - using `v-model` (or using `:model-value="property_name"` and `@update:modelValue="function_name"`) on custom components by using `props: ['modelValue']` and `emits: ['update:modelValue']`
