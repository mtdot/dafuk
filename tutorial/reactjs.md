# Source
[Udemy](https://samsungu.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/25600370#overview)

# Content

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

## 245. Splitting Our Code
 - Separating slices
 - Exporting reducer & reducer actions

## 254. Where To Put Our Logic
 - Where to put async/sync code?
 - [CODE](https://github.com/academind/react-complete-guide-code/tree/19-advanced-redux/code/zz-suboptimal-example-code)

## 258. Using an Action Creator Thunk
 - Thunk: action creator return an function that execute another action later
 - 
## 259. Getting Started with Fetching Data

## 261. Exploring the Redux DevTools

## 263. Module Resources
 - [CODE](https://github.com/academind/react-complete-guide-code/tree/19-advanced-redux)

## 267. Defining & Using Routes
 - Route
 - BrowserRouter

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
 - 
