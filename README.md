# rate_limit

`rate_limit` limits how many requests each client may make, counting requests per key with a fixed window, a sliding window, or a token bucket. It keeps the counters in memory by default or in any store with the methods `incr`, `get`, and `set`. Registered as a `web` plugin, it sets the `RateLimit` headers and answers a request over the limit with status 429.

The following example limits each API key of a web application to 100 requests per minute, then checks a token bucket for one user directly.

```lus nocheck
local rate_limit = require("https://atmosp.here/2.0/rate_limit.lus")

-- 100 requests per minute for each API key.
app:register(rate_limit, {
    window = 60,
    max = 100,
    key = function(req) return req.headers["x-api-key"] end,
})

-- A limiter works without `web` too.
local limiter = rate_limit.new({ algorithm = "bucket", max = 5, window = 1 })
local allowed, info = limiter:check("user:42")
if not allowed then
    print(`retry in $(info.retry_after) s`)
end
```

The package requires Lus 2.0 and declares no permissions. It never calls `pledge`, so the program that loads it keeps control of its permissions.

The reference is in the doc comments of `rate_limit.lus`, which `lus doc rate_limit.lus` prints.
