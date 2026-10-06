<img src="https://raw.githubusercontent.com/komp-co/kf-extensions/main/brand/kiwi.svg" width="96" alt="The KFlat paper kiwi">

# komp-test

KFlat's tests: `testing`, the library tests are written against, and
`komp_test`, the runner for the test programs `komp test` builds. Both are one
package, `komp_test`, in the package index.

## Writing tests

A crate with tests names the library in its dev-dependencies:

```toml
[dev-dependencies]
testing = "0.1"
```

and each `_test.kf` file imports what it uses:

```kflat
import testing.test

@test
fun adds(): void { assert_eq(1 + 1, 2, "one and one") }
```

`testing` declares `@test` and `@disabled`, and `run_tests`, the entry point
of a test program; `komp test` builds a program around it.

## Running test programs

```console
$ komp-test target/kflat/test/app_tests --filter parse
```

Each program named is run with `--filter` passed on, reports its own tests,
and komp-test fails when any of them does.
[komp-co/komp#254](https://github.com/komp-co/komp/issues/254) has where it
is going: listing each program's tests, running each in its own child, in
parallel and under a timeout, and merging the reports across a workspace.

## Building

```console
$ komp test .
$ komp build .
```

`src/lib/` is the `testing` library, `src/bin/` the runner.

MIT licensed.
