<img src="https://raw.githubusercontent.com/komp-co/kf-extensions/main/brand/kiwi.svg" width="96" alt="The KFlat paper kiwi">

# komp-test

The test driver behind `komp test`, written in KFlat and published to the
package index as `komp_test`. komp builds a crate's test program; komp-test
runs it.

```console
$ komp-test target/kflat/test/app_tests --filter parse
```

Each program named is run with `--filter` passed on, reports its own tests,
and komp-test fails when any of them does.

## Where it is going

[komp-co/komp#254](https://github.com/komp-co/komp/issues/254) has the plan:
komp asks for a test build with `komp build --tests`, and komp-test lists each
program's tests, runs each in its own child, in parallel and under a timeout,
and merges the reports across a workspace. core keeps only the `@test`
annotation and the entry point a test program runs
(`core.testing.run_tests`).

komp-test talks to komp and to test programs through their command lines and
JSON, never through the compiler's crates, so it ships without a compiler
release.

## Building

```console
$ komp test .
$ komp build .
```

MIT licensed.
