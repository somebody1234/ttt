# Built-in Utility Types

This is a list of built-in utility types, with the most commonly used types first.

### `Record<Key, Value>`

This represents an object used as a lookup (dictionary), where every value is the same.

Note that if the key is a type with infinite members,
like `string`, or `number`, or `` `a${string}` ``,
every key is implicitly optional, meaning that property accesses results in `Value | undefined`
if [`noUncheckedIndexedAccess`](https://www.typescriptlang.org/tsconfig#noUncheckedIndexedAccess)
is enabled.

[Source Code](https://github.com/microsoft/TypeScript/blob/634d3a1db5c69c1425119a74045790a4d1dc3046/src/lib/es5.d.ts#L1578-L1583)
```ts
type Record<K extends keyof any, T> = {
    [P in K]: T;
};
```
