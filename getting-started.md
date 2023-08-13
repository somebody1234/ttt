# Getting Started

This page details how to get a basic installation of TypeScript up and running.
Specifically, it does not cover tooling choices.

## Add TypeScript as a dependency

Don't rely on a global installation of TypeScript!

```sh
npm i -D typescript
pnpm i -D typescript
yarn add -D typescript
```

## Create a `tsconfig.json` in the project root

See [the page on `tsconfig.json`](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)
in the TypeScript Handbook.

Note specifically the [TSConfig Bases](https://github.com/tsconfig/bases/),
which are a great way to get a `tsconfig.json` that Just Works™️.

## (Optional) Set up for JavaScript

<!-- TODO: find that one article on incremental JS -> TS migrations -->
