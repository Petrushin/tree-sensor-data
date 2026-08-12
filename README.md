# Tree sensor metadata

One JSON file per sensor, named after the ID the beacon broadcasts.
The app requests `{baseUrl}{id}.json`, so sensor 3 fetches `sensors/3.json`.

## Serving these

### Option A — GitHub raw (simplest, works immediately)

Push this folder to a public repo. The files are then served over HTTPS
straight away, with no further setup:

```
https://raw.githubusercontent.com/USERNAME/tree-sensor-data/main/sensors/
```

Set that as `baseUrl` in `SensorInfo.kt`.

Caveat: raw.githubusercontent.com serves with a short cache and is not
meant for production traffic. Fine for a handful of sensors and testing.

### Option B — GitHub Pages (proper static hosting)

Same repo, then **Settings → Pages → Source: main branch**. After a
minute the files are at:

```
https://USERNAME.github.io/tree-sensor-data/sensors/
```

Better caching, a nicer URL, still free. This is what I would use for a
real deployment.

## Adding a sensor

Create `sensors/<id>.json`. Every field is optional — the app skips
anything missing.

```json
{
  "name": "Oak, North Gate",
  "species": "Quercus robur",
  "location": "Parco di Villa Durazzo, Genoa",
  "notes": "Free text shown under the readings.",
  "last_inspection": "2026-03-14",
  "url": "https://example.com/full-record"
}
```

`url` becomes the "Full record" button — the one place a link still
makes sense, since it is an explicit action rather than something
opening unbidden.
