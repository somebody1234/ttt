# Quick Tips
This page lists various tips related to type annotations.
Note that tooling and framework tips are out of scope for this document.

## Never use `any`
Using `any` is basically disabling type checking -
which is probably the opposite of your goal when you're using TypeScript.
It should only be used as a last resort,
when the alternatives (if any exist) are even less desirable.

For example:
- A complicated type that would otherwise require conditional types
  (see the next tip for alternatives)
- Dynamic imports

## Avoid conditional types
Just because a feature exists doesn't mean you should use it for everything.

See alternatives for common usages of conditional types below.

### Simple conditional types
You may be able to use overloads:  
[Open in Playground]()
```ts
function foo<T extends string | number>(it: T): T extends string ? 'string' : 'number' {}

function foo2() {
  //
}
```

## Remember to use `readonly T[]` in function parameters
You should often be using `readonly T[]` in function parameters
if you aren't modifying them.
This is because `readonly T[]` is a parent type of `T[]`,
meaning a `readonly T` argument accepts both `readonly T` and `T`,
whereas a `T` argument doesn't accept a `readonly T`.

(Note: `{ t: 't'; }` and `{ readonly t: 't'; }` are both equivalent in the type system.
See [pc#6532](https://github.com/microsoft/TypeScript/pull/6532#issuecomment-174356151),
[i#13347](https://github.com/microsoft/TypeScript/issues/13347))

You can think of it like this:  
[Open in Playground](https://www.typescriptlang.org/play?#code/C4TwDgpgBAKlC8UDeAoKUBOECGATAFAJQBcUA5MGQNxpQDuGAlsBPsKRWSVAG4D2jXDQC+NUJCgAlHLj4A7ADYg4iVOix4iHSiLHho0vPKUBRAB4s5uAM4A5eYdmKQCKTOPKoECxCvXYUAD8UMAYAK7QpABm2ArWEDQA9InoUAB6gSji0PZyjh7mljb5zq5w3kX+JUpwwaERUNGx8Ukp6BlAA)
```ts
type T = {
  read(): 't';
  write(t: 't'): void;
};
type ReadonlyT = {
  read(): 't';
};
type ReadonlyExtendsNonReadonly = ReadonlyT extends T ? true : false;
//   ^? - type ReadonlyExtendsNonReadonly = false
type NonReadonlyExtendsReadonly = T extends ReadonlyT ? true : false;
//   ^? - type NonReadonlyExtendsReadonly = true
```

## Use `T extends T` instead of `T extends any` or `T extends unknown` for distributive conditional types
They all always succeed, but `T extends T` has some benefits for maintainability:
- avoiding `any` makes it easier to limit your usage of `any` - this also makes linters happy
- `T` is shorter than both `any` and `unknown` -
of course, this doesn't apply if you use long names for your generic parameters
- intuitively, it's a lot easier to guess that `T` always `extends T` -
you don't even need to know what `any` and `unknown` are