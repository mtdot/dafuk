# Template Literals

## Source

[hackerrank](https://www.hackerrank.com/challenges/js10-template-literals/problem)

## Dafuk

```js
function sides(literals, ...expressions) {
  // literals = [ 'The area is: ', '.\nThe perimeter is: ', '.' ]
  // expressions = [int, int]
}


const [x, y] = sides`The area is: ${s1 * s2}.\nThe perimeter is: ${2 * (s1 + s2)}.`;
```

# DayOfWeek's name

## Source

[hackerrank](https://www.hackerrank.com/challenges/js10-date/problem)

## Dafuk

```js
let dayName = new Date(dateString).toLocaleString('en-us', { weekday:'long' })
```

# ReactJS the recommended way to set state (which heavily depend on previous state)

## Source
[Udemy - ReactJS](https://samsungu.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/25596010#overview)

## Dafuk
```js
// declare state
const [data, setData] = useState({
  title: 'counter',
  value: '1'
});

// updating state
const valueChangedHandler = (event) => {
  setData((prevState) => {
    return {...prevState, value: prevState.value + event.target.value}
  });
}
```

# ReactJS proper way for ensuring a value is a Number

## Source

[Udemy - ReactJS](https://samsungu.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/25598410#overview)

## Dafuk
```js
// shortcut for ensuring 'enteredValue' is a number
if (+enteredValue > 0) {
  // ...
}
```

# ReactJS useEffect's clean-up function doesn't just run once

## Source

> Additionally, if a component renders multiple times (as they typically do), 
> the previous effect is cleaned up before executing the next effect

## Dafuk

First Run   : `Render` > `Effect` > (Preparing Cleanup Function)

Second Run  : `Render` > `Cleanup` (from previous Effect) > `Effect` > (Preparing New Cleanup Function)


# js destructuring with assignment alias

## Source

[Udemy - ReactJS](https://samsungu.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/25599236#overview)

## Dafuk

```js
const state = {
  isValid: true,
  name: 'abcxyz'
}

const { isValid: isNameValid } = state; // unpacking property 'isValid' of 'state' object, then assign as variable with name 'isNameValid'

```

# js bind() method

## Source

[javascripttutorial](https://www.javascripttutorial.net/javascript-bind/)

## Dafuk

```js
const sum = (a, b) => a + b

// the original way
sum(1, 2) // expected output '3'

// the 'bind' way
sum.bind(null, 1)(2) // same output as original way
```

