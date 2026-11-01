# Verona Base

Core macros, protocols, and primitive type instances for the Verona programming language.

The current package version is declared in `verona.build`.

## Build

With a compatible Verona compiler available:

```sh
verona build base ./build
```

Add this repository's `src` directory to a consuming project's module paths and
import `base`. Base has no Verona library dependencies.

## Conditional expressions

`base:cond` selects the first true clause, evaluating tests once in source order
and running only the selected body. Each clause has a boolean test and a nonempty
body; its final expression supplies the result.

```lisp
(import base)

(base:function choose ((ready bool) (retry bool)) i64
  (base:cond
    (ready 42)
    (retry 7)
    (true 0)))
```

A final literal `true` is the default for value-producing choices. Without a
default, falling through returns `unit`, so all branches must also return unit.
`(base:cond)` returns unit. Branch types must agree, and all bodies are checked,
even when a preceding clause is always true. Empty clauses, missing bodies and
nonboolean tests are errors. The macro expands to existing `match`/`do` forms
without introducing runtime local names. This is runtime library syntax; the
compile-time evaluator's `cond` retains its existing behavior.

## Tests

The bounded-value tests depend on the Testing library. Place the Testing source
checkout beside this repository as `testing/`, then run:

```sh
cd tests
verona build bounded-tests ../build
../build/bounded-tests
```

The `base-*-client.vrn` files are compiler integration fixtures exercised by the
main Verona repository's frontend suite. When checked out as `projects/base`
inside Verona, run `make test-frontend` and `make test-bounded` from Verona's root.

## Development

This repository is included at `projects/base` as a pinned submodule of
[Verona](https://github.com/verona-project/verona). Public clones use HTTPS.
For SSH pushes in a development checkout:

```sh
git remote set-url --push origin git@github.com:verona-project/base.git
```

Released under the Unlicense; see `LICENSE`.
