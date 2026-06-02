Title: `Validate` panics on nil request in `handlers/auth.go`

The `Validate` function in `handlers/auth.go:42` reads `req.Headers["X-Token"]` without first checking that `req` is non-nil. The upstream middleware in `handlers/middleware.go:88` is allowed to hand in a nil pointer when the body parser fails, so a malformed request crashes the goroutine for that connection instead of returning a clean 400.

```go
func Validate(req *Request) error {
    token := req.Headers["X-Token"]
    ...
}
```

`Validate` is the last guard before the token is read, and the panic propagates past the recovery layer in `server.go:120`, which only wraps the request loop — not the handler stack itself.

A two-line check at the top of `Validate` — `if req == nil { return errBadRequest }` — turns the crash into a normal error path; the existing test in `auth_test.go:71` should be extended with a nil-input case so the guard never silently disappears.
