Title: Parser drops trailing newline in `parse.go`

The `Parse` function in `src/parser/parse.go:78` strips the last byte of every input that ends in `\n`, because the loop guard reads `i < len(input) - 1` instead of `i < len(input)`. Files without a trailing newline are parsed correctly, but files that do end in one lose their final character before tokenization.

```go
for i := 0; i < len(input)-1; i++ {
    tokens = append(tokens, input[i])
}
```

The formatter in `src/format/emit.go:204` consumes the parser's output verbatim, so every formatted file ends up missing the newline it came in with, and a noisy diff lands on every save.

Changing the guard back to `i < len(input)` fixes the off-by-one without touching anything else; the table-driven test in `parse_test.go:155` should grow one more case whose input ends in `\n` so the regression is locked down.
