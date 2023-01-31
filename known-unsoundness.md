# Known unsoundness
This page lists parts of TypeScript that are (usually intentionally) unsound.
This usually happens when the benefits outweigh the unsoundness.

## Explicit unsoundness

### `declare`
Unsound if the value doesn't exist.

### `!`
Turns `T | null | undefined` into `T`.  
Unsound if the value is actually `null` or `undefined`.

### Type casts (`<T> val` and `val as T`)
Unsound if `val` is not actually `T`.

## Function overloads
Each overload must be assignable to the implementation signature
(the signature attached to the function body).  
Note that functions without a body do not have an implementation signature.
For these functions, overloads cannot be checked at all.  
Unsound