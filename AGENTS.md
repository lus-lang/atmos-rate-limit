# AGENTS.md

`lus-lang/atmos-rate-limit` is the repository of the `rate_limit` package of the atmosphere registry. Programs load the package with `require("https://atmosp.here/2.0/rate_limit.lus")`.

## Scope

`rate_limit` limits how many requests each client may make, counting requests per key with a fixed window, a sliding window, or a token bucket. It keeps the counters in memory by default or in any store with the methods `incr`, `get`, and `set`. Registered as a `web` plugin, it sets the `RateLimit` headers and answers a request over the limit with status 429. The public API is every function that `rate_limit.lus` returns in its module table. A change to that API needs a new entry in `CHANGELOG.md` and a version change in the header.

## Layout

- `rate_limit.lus` is the whole package. Its header doc comment contains the package metadata and the declared permissions.
- `tests/*_test.lus` are the tests. They load `rate_limit.lus` from the parent of `TEST_DIR`, the directory that holds the test file.

The tests load `web` from a checkout of `lus-lang/atmos-web` next to this repository, so clone it into the same parent directory first.

## Commands

Run these commands from the root of the repository.

```sh
lus test tests          # run the tests
lus check rate_limit.lus     # lint, including the package codes
lus doc rate_limit.lus       # print the reference
```

## Rules

- Every public function has a doc comment that states each result and each error, following `spec/design/style.md` of the Lus repository.
- The package never calls `pledge`. A new permission is declared in the header and in the README.
- Prose follows the `lus-writing` skill, which `lus agents init` installs and https://lus.dev/agents/skills/lus-writing/SKILL.md serves. In particular, prose has no dashes or semicolons and never names the Roblox Lua dialect.
- Every bug fix comes with a test that fails without it.
