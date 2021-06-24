# Source
[Udemy](https://samsungu.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/25600370#overview)

# Content

## 102. React Fragments
 - Understanding fragments component & how it work

## 104. Working with Portals
 - Understanding portals concept & how to apply

## 105. Working with "ref"s
 - Should use only to get value from `input`
 - Avoid manipulate value of DOM element, let it manipulate via `state`

## 124. `Refactoring` Building & Using a Custom Context Provider Component
 - Understanding Custom Context Provider
 - Knowing limitations for high frequence changes

## 154. `Optimization` Preventing Unnecessary Re-Evaluations with `React.memo()`
 - Caching components

## 156. `Optimization` `useCallback()` and its Dependencies
 - Caching methods

## 160. `Optimization` Optimizing with `useMemo()`
 - Caching objects

## 190. `Refactoring` Building a Custom Http Hook
 - Understanding custom hook for http request

## 205. `Refactoring` BAdding A Custom Input Hook
 - Understanding custom hook for input field

## 232. Providing the Store

## 233. Using Redux Data in React Components
 - useSeletor() hook

## 234. Dispatching Actions From Inside Components
 - useDispatch() hook
 - reducer actions
 - action payload

## 240. Adding State Slices
 - useSice() hook

## 242. Migrating Everything To Redux Toolkit

## 243. Working with Multiple Slices

## 245. `Refactoring` Splitting Our Code
 - Separating slices
 - Exporting reducer & reducer actions

## 254. Where To Put Our Logic
 - Where to put async/sync code?
 - [CODE](https://github.com/academind/react-complete-guide-code/tree/19-advanced-redux/code/zz-suboptimal-example-code)

## 258. Using an Action Creator Thunk
 - Thunk: action creator return an function that execute another action later

## 259. Getting Started with Fetching Data

## 261. Exploring the Redux DevTools

## 263. Module Resources
 - [CODE](https://github.com/academind/react-complete-guide-code/tree/19-advanced-redux)

## 267. Defining & Using Routes
 - Route
 - BrowserRouter

 > Potential issue with Route with urls with same suffix. Ex: `/products` & `/products/:productId` will be both trigged.

## 268. Working with Links
 - Link
 - Link vs Route
 
 > `Link` component is responsible for the transition (including registerring & transitioning) from state to state (page to page), while the `Route` component is responsible to act as a switch to display (serving) certain components based on route state.

## 269. Using NavLinks
 - Link vs NavLink
 > `NavLink`: A special version of the `Link` that will add styling attributes to the rendered element when it matches the current URL.
 
 - Sample Code
 ```jsx
 <Link to="/">Home</Link>
 <NavLink to="/" activeClassName="active">Home</NavLink>
 ```

## 270. Adding Dynamic Routes with Params
```jsx
<Route path="/abcxyz/:productId">Product</Route>
```

## 271. Extracting Route Params
 - useParams() hook

## 272. Using "Switch" and "exact" For Configuring Routes
 - `Switch`: map & serve first url fit with `Route`
 - `Switch` without `exact`: map using startsWith
 - `Switch` with `exact`: map using exact same url

## 273. Working with Nested Routes
 - Understanding concept of Nested Route & how it evaluated - ? Confusing ...
 - useRouteMatch() hook
 ```
 let { path, url } = useRouteMatch();
 ```
 > Consider the route `/users/:userId`. `match.path` would be `/users/:userId` while `match.url` would have the `:userId` value filled in, e.g. `users/5`.

## 274. Redirecting The User
 - `Redirect` component: Automatically redirect to specific url when accessing specified url

## 281. Adding a "Not Found" Page

```jsx
<Switch>
    <Route path="..."> ... </Route>
    // ... apps routes
    <Route path="*"> // fallback route 
        <NotFound />
    </Route>
</Switch>
```

## 282. Implementing Programmatic (Imperative) Navigation
 - useHistory() hook
 - Different between history.push() & history.replace(): `push` can go back with BACK button of browser, `replace` cannot
 - `Tips`: for authentication page, `history.replace('/')` is good~

## 283. Preventing Possibly Unwanted Route Transitions with the "Prompt" Component
 - `Prompt` component. Making confirmation when leaving editting form. 

## 284. Working with Query Parameters
 - `useLocation()` hook
 - `location.search`
 - `URLSearchParams` class
 - `queryParams.get()` to access queries.
 - Different between `match.url` and `location.pathname`
 > `match.url`: take from `<Route path="..."></Route>`
 
 > `location.pathname`: relative path with root path

 - Using `history.push()` with object `{pathname: '...', search: '...'}

## 287. Sending & Getting Quote Data via Http
 - separating api to specific file

## 292. `Optimization` Adding Lazy Loading
 - `React.lazy()`
 - `Suspense` component
 - Avoid `Layout` and `Progress bar` component

## 295. Exploring Routing Issues & Finishing Deployment
 - Understanding configure single page app [stackoverflow](https://stackoverflow.com/questions/37667626/firebase-cli-configure-as-a-single-page-app-rewrite-all-urls-to-index-html)

## 308. `Security` Protecting Frontend Pages
 - Protect all main routes with `isLoggedIn` from `AuthContext`
 - Redirect to `/auth` if need (ex: need login to view the page)
 - `Again` Refer section `281` for adding a "Not Found" Page

## 309. Persisting The User Authentication Status
 - using `localstorage` to persisting authentication token

## 310. Adding Auto-Logout
 - handling expired token by using `setTimeout` for calling `logout` base on `remainingTime`

## 311. Finishing Steps
 - complete auto-logout steps

# NEXTJS

## 322. Creating Dynamic Pages (with Parameters)
 - Understanding path, nested path concepts: by `filename.js`, by `foldername/index.js`, by `foldername/nested-path.js`, by `foldername/nested-folder/index.js`
 - Understanding dynamic path (parameters): by `[newsId].js`, by folder `[newsId]/index.js`
 - Understanding `useRouter()` hook: `const router = useRouter()`, `const newsId = router.query.newsId;`
 - `Link` component from `next/link`

## 329. The "_app.js" File & Layout Wrapper
 - layout

## 330. Using Programmatic (Imperative) Navigation
 - `useRouter()` hook to `push` navigation

## 333. Data Fetching for Static Pages
 - Only use SSG on page components (that belong to nextjs, not reactjs component)
 - Static site pre-rendering with `getStaticProps()`

## 334. More on Static Site Generation (SSG)
 - `revalidate: 10` property indicate the number of seconds the static page should be re-generated

## 335. Exploring Server-side Rendering (SSR) with `getServerSideProps`
 - For serve content changed with every request (multiple times per second), understand when to use SSG, when to use SSR
 - Should be some fetching data from API or file system
 - Using `context` parameter to access `context.req` & `context.res`

## 336. Working with Params for SSG Data Fetching
 - Accessing URL parameter via `context` param of `getStaticProps(context)`
  > const newsId = context.params.newsId;

## 337. Preparing Paths with "getStaticPaths" & Working With Fallback Pages
 - Combining `getStaticPaths()` with `getStaticProps(context)`
 - Understanding `paths` property of returning object from `getStaticPaths()`: define available paths
 - Understanding `fallback` property of returning object from `getStaticPaths()`
  > `false` => 404 if path not available. [Code](https://nextjs.org/docs/basic-features/data-fetching#fallback-false)
  > `true`  => return the page in fallback state, using `const router = useRouter(); if (router.isFallback) { ... }` for waiting
  > `blocking` => same as `true` but browser will wait for SSR done, then render the page

## 338. Introducing API Routes
 - api seems similar with expressjs

## 340. Sending Http Requests To Our API Routes
 - using the internal implemented api

## 341. `NextJS` `BE` Getting Data From The Database
 - Fetching data from DB

## 343. Adding "head" Metadata
 - `Head` component from `next/head`
 - Know which head metadata should be add to website
 - Add different metadata for each 'root' pages

## 382. Understanding the Technical Setup & Involved Tools
 - test library already setup with command `create-react-app`

## 385. Grouping Tests Together With Test Suites
 - Unit test for component & groupping testcases
 - `getByRole()`

## 388. Testing Asynchronous Code
 - Unit test for `async` methods by implement `async` test case
 - `findAllByRole()` with `await` and `timeout`: default `timeout` is 1s

## 389. Working With Mocks
 - Mocking api with `jest`
 -

# ReactJS + TytpeScript

## 405. Working with Props & TypeScript
 - type inference with `React.FC<{ items: string[] }>` of functional component
 - this type inference also support for auto completion feature of IDE

## 408. Form Submissions In TypeScript Projects
 - handle form submit with `React.FormEvent`
 > const submitHandler = (event: React.FormEvent) => { }

## 409. Working with refs & useRef
 - refs with `HTMLInputElement`
 > const inputRef = useRef<HTMLInputElement>(null);

## 410. Working with "Function Props"
 - Generic type for function
 ```ts
 const NewTodo: React.FC<{
  onAddTodo: () => void
 }> = (props) => {}
 ```

