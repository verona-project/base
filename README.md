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
