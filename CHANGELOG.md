# Changelog

## 1.0.0

**Release date:** TBD

Version 1.0.0 is the first release of `rate_limit`.

- Added the `rate_limit` package.
  - `rate_limit.new`: Creates a limiter that counts requests per key with a fixed window, a sliding window, or a token bucket.
  - `rate_limit.memory`: Creates a store that keeps the counters in the memory of the process.
  - `rate_limit.forwarded`: Returns a key function that reads the client address from the `X-Forwarded-For` header.
  - `rate_limit.register`: Registers a limiter on a `web` scope, which sets the `RateLimit` headers and answers a request over the limit with status 429.
