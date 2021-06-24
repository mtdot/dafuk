## union type

```ts
let a: string | number = "abc";
let b: string | number = 10;

function padLeft(value: string, padding: string | number): string | number {
  // ...
}
```

## type alias

```ts
type Second = number;

type Person = {
  name: string;
  age: number;
}

```

## Generic

```ts
function insert<T>(array: T[], value: T): T[] {
  const newArray = [value,...array];
  return newArray;
}

```
