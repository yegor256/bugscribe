Title: `parse_iso` reads timestamps in local time in `utils/dates.go`

The `parse_iso` helper in `utils/dates.go:51` calls `time.Parse(layout, s)` without naming a location, so the returned `time.Time` is interpreted in the host's local zone. Every other layer of the pipeline — the metrics aggregator in `metrics/bucket.go:34` and the dashboard query in `dashboard/range.go:19` — assumes the timestamps are already in UTC.

```go
func parse_iso(s string) (time.Time, error) {
    return time.Parse(layout, s)
}
```

Production runs in `America/New_York`, so the four-hour offset shifts every hourly bucket; the "last 24 hours" panel on the ops dashboard is consistently stale by exactly that offset, and the off-by-one only disappears twice a year when daylight saving lines up.

Replacing the call with `time.ParseInLocation(layout, s, time.UTC)` keeps the same signature and removes the drift; the existing tests in `dates_test.go:33` use a fixed-UTC fixture and miss this, so one more case with a non-UTC-looking string should be added to lock the behavior down.
