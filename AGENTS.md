# uuidchop

**What it does:** Browser-side UUID generator, validator, and inspector. Generate v4 UUIDs, validate any UUID string, and decode v1 timestamps — all in-browser via the Web Crypto API.

## Capabilities

| Capability | Description |
|------------|-------------|
| Generate UUID v4 | Cryptographically secure random UUID using `crypto.randomUUID()` |
| Bulk generate | 1–100 UUIDs at once, exportable as plain text |
| Validate | Check any UUID string for format correctness |
| Inspect version | Detect UUID version (1–5) and variant from the UUID bytes |
| Decode v1 timestamp | Extract the embedded timestamp and MAC bytes from a v1 UUID |

## Human surface

**URL:** https://uuidchop.radicchio.page

Two-tab UI:
- **Generate** — pre-generated UUID on load, copy button, bulk generation (1–100), download as .txt
- **Validate** — paste any UUID, instant feedback: valid/invalid, version, variant, v1 timestamp

## Input/output

**Generate** (browser-side, no input required):
```
Output: 550e8400-e29b-41d4-a716-446655440000
Format: lowercase hyphenated UUID v4
```

**Validate** (browser-side):
```
Input:  any string (normalises compact/uppercase variants)
Output: { valid: bool, version: int, variant: string, timestamp?: string, macBytes?: string }
```

## Agent usage

This tool is currently browser-only. Agents can use UUIDs directly via platform APIs:

**Node.js / Deno / modern browsers:**
```js
const uuid = crypto.randomUUID(); // built-in, no library needed
```

**Validate in Node.js:**
```js
const UUID_RE = /^[0-9a-f]{8}-[0-9a-f]{4}-[1-5][0-9a-f]{3}-[89ab][0-9a-f]{3}-[0-9a-f]{12}$/i;
const isValid = UUID_RE.test(uuid);
```

A JSON API endpoint is planned for agents that need programmatic UUID generation or validation without running their own crypto:

```
GET https://uuidchop.radicchio.page/api/generate?count=10&version=4
→ { "uuids": ["...", "..."] }

POST https://uuidchop.radicchio.page/api/validate
Body: { "uuid": "550e8400-e29b-41d4-a716-446655440000" }
→ { "valid": true, "version": 4, "variant": "RFC 4122" }
```

*API not yet live — planned for Tier 2 deployment on Cloudflare Workers.*

## Pricing

Free. The browser-side tool is complete and unlimited. No signup required.

Planned paid tier: bulk API access (1000+/request), namespace seeding, team API keys — $4/month or $19 lifetime.

## Privacy

All computation runs in the browser. No UUIDs are transmitted. No analytics on individual UUIDs.

## Related tools

- [hashchop](https://hashchop.radicchio.page) — SHA-256/512 hash generator
- [jwtchop](https://jwtchop.radicchio.page) — JWT token decoder
- [b64chop](https://b64chop.radicchio.page) — Base64 encoder/decoder
- [csvchop](https://csvchop.radicchio.page) — CSV inspector and JSON converter

## Support

https://bitterdesk.com/s/uuidchop/
