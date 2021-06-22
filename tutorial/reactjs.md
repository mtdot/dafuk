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
