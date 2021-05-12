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

[hackerrank]()

## Dafuk

```js
let dayName = new Date(dateString).toLocaleString('en-us', { weekday:'long' })
```
