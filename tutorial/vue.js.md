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
  - Interpolation syntax `{{ doSomething() }}` for evaluating method: This should be avoid, because `doSomething()` as `methods` alway be executed when anything on the page changed.
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

## 154. Getting Data (GET Request) & Transforming Response Data
  - Using `fetch` should chain the promise with arrow function to avoid error related to `this.property`
  - When using `fetch` to POST, PUT, GET, DELETE, we should validate the response status code via `response.ok`

## 155. Loading Data When a Component Mounts
  - `mouted()` lifecycle

## 165. Registering & Rendering Routes
  - register via `createRouter`, `createWebHistory` hook from `vue-router` package
  - Using `<router-view>` tag to render component
  - Using `<router-link to="/teams">` to navigate between paths
  - styling using class name `router-link-active` & `router-link-exact-active`: for example: https://host/teams (match by both) & https://host/teams/team1 (match by `router-link-active`)
  - class name can be overwite with othername by settings attribute `linkActiveClass="active"` & `linkExactActiveClass="exact-active"`
```
import { createApp } from 'vue';
import { createRouter, createWebHistory } from 'vue-router';

const router = createRouter({
  history: createWebHistory(),
  routes: [
    {
      path: '/teams',
      component: TeamList
    },
    { path: '/users', component: UserList }
  ]
});
const app = createApp(App);
app.use(router);
```
  - Modify scroll behavior
```
scrollBehavior(to, from, savePosition) {
  if (savePosition) {
    return savePosition;
  }
  return {top: 0, left: 0};
}
```

## 168. Programmatic Navigation
```
this.$router.push('/teams');
this.$router.back();
this.$router.forward();
```

## 169. Passing Data with Route Params (Dynamic Segments)
```
// register path
{ path: '/teams/:teamId', component: TeamMembers }

// access parameter
this.$route.params.teamId
```

## 170. Navigation & Dynamic Paths
  - dynamic link using `<router-link :to="`/teams/${id}`">` or `computed` method return the link

## 172. `Bug` Updating Params Data with Watchers
  - Knowing the issue while using link `/teams/t2` on page `https://host/team/t1` (will not work because of dynamic link matcher)
  - Knowing the workaround for this issue by adding watcher for `$router`

## 173. Passing Params as Props
  - Passing dynamic route to props of component by using `props: true` in path definition

## 174. Redirecting & "Catch All" Routes
  - using `redirect: '<other_path>'` to redirect path to other path (with changing URL to target URL)
  - using `alias: '<other_path>'` to define alternative path to reach component (keeping URL as alias)
  - Catch all other router using
  ```
  { path: '/:notFound(.*)', redirect: '/teams' }
  ```
  
  - Using nested router with `chilrden` property and adding `<router-view></router-view>` to parent component
  - Assigning `name` to path, passing parameters to `path` object
  ```
  // assign name
  { name:'team-members', path: ':teamId', component: TeamMembers, props: true },
  
  // using path by name with passing parameters
  <router-link :to="{ name: 'team-members', params: { teamId: id } }">
    View Members
  </router-link>
  ```
  - Passing queries
  ```
  <router-link :to="{ name: 'team-members', params: { teamId: id }, query: { sort: 'asc' } }">
    View Members
  </router-link>
  ```
  - Using `query` by `this.$route.query`

## 178. Rendering Multiple Routes with Named Router Views
  - named router view `<router-view name='footer'></router-view>`
  - `router-view` without name equals to `<router-view name='default'></router-view>`
  - Multiple components for path via `components: { default: TeamsList, footer: TeamsFooter }` (NOT `component`)
  ```
  { path: '/users', components: { default: UsersList, footer: UserFooter } },
  ```
  - Vuejs will render nothing for named `router-view` if we not pass anything for that named `router-view`

## 180. Introducing Navigation Guards
  - Using `router.beforeEach(to, from, next)` for `Global Guard`
  ```
  router.beforeEach(to, from, next) {
    if (someCondition) {
      next(false);
    }
    // or next(true)
    // or next('/users') => redirect
    // or next({name: 'teams-members', params: { teamId: id }}) => redirect with named router
    next(); 
  }
  ```
  - Using `beforeEach(to, from, next)` on single path for `Route Config Level Guard`
    ```
    { 
      path: '/users', 
      components: { default: UsersList, footer: UserFooter },
      beforeEach(to, from, next) {
        // handle logic
      }
    },
    ```
  - Using `beforeRouteEnter(to, from, next)` hook on component for `Component Level Guard`
  - The order: `Global Guard` >> `Route Config Level Guard` >> `Component Level Guard`
  - `beforeRouteUpdate(to, from, next)` hook on component called when re-use the component with other `route` (or parameters)
  - `router.afterEach(to, from)` called after each routing. for send analytics ...
  - `beforeRouteLeave(to, from, next)` hook on component for `Making confirmation when leaving editting form ` (same as `Prompt` compoent on ReactJS)
  ```
  beforeRouteLeave(to, from, next) {
    const userWantToLeave = confirm("Do you really want to leave?");
    next(userWantToLeave);
  }
  ```
  - Defining metadata for path
  ```
  { 
    path: '/users', 
    meta: { needAuth: true },
    components: { default: UsersList, footer: UserFooter },
    beforeEach(to, from, next) {
      // handle logic
      if (to.meta.needAuth) {
        // redirect to auth page
        next('/login');
      }
      next();
    }
  },
  ```
## 185. Organizing Route Files
  - Seperate all router definition to `router.js` file

## 209. Creating & Using a Store
  - Why `Vuex`: replacing `provide`/`inject` mechanism
  - Managing states like ReactJS

## 211. `Bug` Introducing Mutations - A Better Way of Changing Data
  - Synchronizing state mutations (prevent race conditions)
  - Declaring & Using mutation methods
  ```
  const store = createStore({
      state() {
          return {
              counter: 0
          }
      }, 
      mutations: {
          increment(state) {
              // return {...state, counter: state.counter + 1}
              state.counter = state.counter + 1;
          },
          increase(state, payload) {
              state.counter = state.counter + payload.value;
          }
      }
  });
  
  // using on component
  export default {
      methods: {
          addOne() {
              this.$store.commit('increment');
              this.$store.commit('increase', { value: 10 });
              this.$store.commit({
                type: 'increase',
                value: 10
            });
          }
      }
  }
  ```
## 213. Introducing Getters - A Better Way Of Getting Data
  ```
  getters: {
      finalCounter(state) {
          return state.counter * 2;
      },
      normalizedCounter(state, getters) {
          const finalCounter = getters.finalCounter;
          if (finalCounter > 100) {
              return 100;
          }
          return finalCounter;
      }
  }
  
  // accessing on component
  this.$store.getters.finalCounter;
  this.$store.getters.normalizedCounter;
  ```
## 214. Running Async Code with Actions
  - action should be same name with mutation method due to `component` -> `action` -> `mutation`
  - action can dispatch other action via `context`
  
## 216. Using Mapper Helpers
  - Automatically merge getters into `computed` sections by `mapGetters`
  
  ```
  <template>
    <h3>{{ counter }}</h3>
  </template>

  <script>
  import { mapGetters } from 'vuex';

  export default {
    computed: {
      // counter() {
      //   return this.$store.getters.normalizedCounter;
      // }
      //...mapGetters() // map all
      //...mapGetters([finalCounter]) // using default alias name
      ...mapGetters({
        counter: 'finalCounter' // with alias
      })
    }
  };
  </script>

  ```
  - Automatically merge actions into `methods` sections by `mapActions`
  ```
  <template>
  <button @click="increment">Add 2</button>
  <button @click="increase({ value: 4 })">Add 4</button>
</template>

<script>
import { mapActions } from 'vuex';

export default {
  methods: {
    // addOne() {
    //     // this.$store.commit({
    //     //     type: 'increase',
    //     //     value: 10
    //     // });
    //     this.$store.dispatch('increment');
    // }
    ...mapActions(['increment', 'increase'])
  }
};
</script>
  ```

## 218. `Refactoring` Organizing your Store with Modules
  - Seperate related part of main store into module
  - Seperate module work as local module (CANNOT access `state`, `mutations`, `actions`, `getters` from Global store)
