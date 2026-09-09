# CDN throughput test payloads

Public seed repository for serving static speed-test files through
[jsDelivr](https://www.jsdelivr.com/).

## Contents

| File | Size | Description |
|---|---|---|
| `files/test1_10mb.ai` – `test4_10mb.ai` | 10,000,000 bytes each | Primary payloads |
| `files/calib_05mb.ai` | 5,000,000 bytes | Short payload |
| `files/calib_20mb.ai` | 20,000,000 bytes | Long payload |
| `files/opendata_*.ai` | 2.3 – 5.1 MB | Public government open-data documents |

## Design notes

**Why `.ai`?** Every file is a valid PDF. The `.ai` extension prevents browsers from
rendering it inline, so a click always triggers a download instead of a preview.
jsDelivr does not support custom response headers, so the file extension is the only
available way to force download behaviour there.

**Why random padding?** Each synthetic payload embeds an incompressible random stream,
so gzip and brotli cannot shrink it. Measured throughput therefore reflects real wire
speed rather than a compression ratio.

**Why exact byte counts?** `Content-Length` is then guaranteed accurate, which makes
client-side throughput measurement straightforward to verify.

## Usage

```
https://cdn.jsdelivr.net/gh/<user>/<repo>@<tag>/files/test1_10mb.ai
```

Always pin a git tag (for example `@v1.0.0`). Branch names receive a short cache TTL;
tags are cached permanently and serve considerably faster.

## Contents and licence

`opendata_*` files are public open-data publications from the governments of Australia,
Ireland, Israel, Latvia and Slovenia. `test*` and `calib*` files are synthetic and
contain no meaningful content.
