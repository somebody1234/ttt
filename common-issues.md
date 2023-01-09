# Common Issues
You can guess what this page contains.

## the other kind of includes
## unsafekeyof

## My function is `((x: number) => void) | ((x: string) => void)`, why can't I use it?
The union `|` operator means that your function is either of those two types, and you don't know which.
That means the only ways you can call it, are with arguments that both functions can accept.

In this case, you must provide one argument that is a `number`, but is also a `string`. This doesn't exist

In computer science terms, functions are contravariant ([Wikipedia](https://en.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science)#Function_types)) in their argument types.

## My object `o` has type `{ a: number; } | { a: number; b: number; }`, why can't I access `o.b`?
If it's `{ a: number; }`, then it doesn't have a property `b` and accessing `o.b` is an error.

To be able to access it, you have to narrow it so that `b` is on the object.

One way is by using the `in` operator:  
[Open in Playground](https://www.typescriptlang.org/play?#code/DYUwLgBAhghAXBA3tBA7ArgWwEYgE4DcEAvhAD5IoQY75HZpa6EkEBQUAdNuwJYBmEABQBybCIi9U0AJRI2EaN3aKA9KoB6AfjbEgA)
```ts
let a!: { a: number; } | { a: number; b: number; };
a.b;
//^ error, `b` is not guaranteed to exist
if ('b' in a) {
  a.b;
  //^? - (property) b: number
}
```

Another way is turn it into an optional property instead,
either by manually creating the desired type with optional properties,
or by using the `Partial<T>` helper type.

[Open in Playground](https://www.typescriptlang.org/play?#code/DYUwLgBAhghAXBA3tBA7ArgWwEYgE4DcE2A-GlroRAL4EBQok28SKEGO+R1EAZBAAUoeMAEsowADzIo5TlWxzK3AHz0oAOmz0A9DoB6JOti26DR0QDMIACk3YAlEjoRoplxD2G61Oldsmjs6ugfSuXkbUQA)
```ts
let a!: { a: number; b?: number; };
let b!: { a: number; } & Partial<{ a: number; b: number; }>;
a.b;
//^? - (property) b?: number | undefined
b.b;
//^? - (property) b?: number | undefined
if (a.b) {
  a.b;
  //^? - (property) b?: number
}
if (b.b) {
  b.b;
  //^? - (property) b?: number
}
```

## idk, some function inference problems

## common conditional types problems
