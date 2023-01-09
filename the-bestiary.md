# The Bestiary
This page contains various helper types and useful constructs.

Note that in general, needing advanced types like these
are an indication that you're trying to get TypeScript to do too much.

## Type maps
```ts
type TypeMap = {
  foo: Foo;
  bar: Bar;
};
```

## `NoInfer<T>`
[Open in Playground](https://www.typescriptlang.org/play?#code/C4TwDgpgBAcg9gSQHYDMICcA8AVAfFAXigG1sBdUqCAD2AiQBMBnKAVyQGsk4B3JKAPxQADFABcUJBABuGMgG4gA)
```ts
type NoInfer<T> = [T][T extends unknown ? 0 : never];
```
This type prevents TypeScript from using that location to infer `T` in a generic.

[Open in Playground](https://www.typescriptlang.org/play?#code/C4TwDgpgBAcg9gSQHYDMICcA8AVAfFAXigG1sBdUqCAD2AiQBMBnKAVyQGsk4B3JKAPxQADFABcUJBABuGMgG4AUIoYQAxgBsAhumgp2a4AEs4-BolQYACjq0BbHLgAU1CdgCUbpas069B41NJCzR0G3R7RxcJeGRQx08obCU1UyZgKGoARgkAIzg4DQgtfiJzOOtbOycs9xS0jOoAJjyCopLCYIqwqpq6xVSkdMyAZk7ubvD7PqUAelmoRagAPQFlH21dKH0kQxMzEIwAeVyAK3VgKNcoAG8oLS8oXMeAX0TklXVN-13A-gnLOgTudDFcJHcHrBDlg8PInq93vUho0ACydcqA4EXJwQiQAciyeIANPCoE0oG85gslqsBg1MgBWcbQrGGHH3fGEknPMkU-rzJYrARAA)
```ts
declare function doInferParam<T>(x: T): T;
declare function noInferParam<T>(x: NoInfer<T>): T;
const x1: boolean = doInferParam(1);
//    ^^ error here - T is `number`
const x2: boolean = noInferParam(1);
//   error here - T is `boolean` ^
const x3 = noInferParam(1);
//    ^? - const x3: unknown
// Note that this doesn't error because TypeScript defaults
// any parameter it can't infer to `unknown`, which typechecks fine in this case.

declare function doInferObject<T>(x: { a: T; b: T; }): T;
declare function noInferObject<T>(x: { a: NoInfer<T>; b: T; }): T;
const x4 = doInferObject({ a: '1', b: 2 });
//    ^? - const x4: string        ^ type error here, `T` is inferred from `a`
const x5 = noInferObject({ a: '1', b: 2 });
//    ^? - const x5: number
//                         ^ type error here, `T` is inferred from `b`
```

## `UnionToIntersection<T>`
[Open in Playground](https://www.typescriptlang.org/play?#code/C4TwDgpgBAqgdgSwPZwCpIJJ2BATgZwgGNhk4AeGAPigF4oAKGKCADxzgBN9YoB+RgFcAXLACUdGgAYoouBABueCWw7dGCUQjgAzPFAwTa0-lACi7XAEMS5DABpYNOYrwBuIA)
```ts
type UnionToIntersection<U> = (U extends U ? (u: U) => 0 : never) extends (i: infer I) => 0 ? Extract<I, U> : never;
```

## `IsEqual<T, U>`
[Open in Playground](https://www.typescriptlang.org/play?#code/C4TwDgpgBAkgzgUQI4FcCGAbAPAFQDRQCqAfFALxQAUWAasZQJTmk1QQAewEAdgCZxQcUAPxQA5GjFQAXOIBGYphy58B1Oo2ZRWynvyIjxkmfMWHgAJxTRZAM0xwIAbiA)
```ts
type IsEqual<T, U> = (<V>() => V extends T ? 'a' : 'b') extends (<V>() => V extends U ? 'a' : 'b') ? true : false;
```