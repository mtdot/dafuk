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
  title: 'abcxyz',
  value: '123456'
});

// updating state
const titleChangedHandler = (event) => {
  setData((prevState) => {
    return {...prevState, title: event.target.value}
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
