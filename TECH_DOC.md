# Technical Documentation — Profiler Viewer

## JSON trace format

The viewer expects an array (or a single object) at the root. Each node:

```json
{
  "name": "MyNamespace::MyMethod",
  "totalMs": 123.456,
  "selfMs": 12.34,
  "callCount": 5,
  "children": [ /* recursive */ ]
}
```

| Field | Type | Description |
|---|---|---|
| `name` | string | Display name; use `Namespace::Method` for colour grouping |
| `totalMs` | number | Inclusive (wall-clock) time in milliseconds |
| `selfMs` | number | Exclusive time (totalMs minus all children) |
| `callCount` | number | Number of invocations |
| `children` | array | Nested call nodes (optional) |

## Architecture

* JSON parsing runs in a **Web Worker** so the UI never freezes.
* Tree nodes are built **lazily** — only expanded nodes get DOM elements.
* Tested with files up to 50 MB / 100 000 nodes.
