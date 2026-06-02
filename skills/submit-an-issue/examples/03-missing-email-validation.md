Title: `register` accepts empty email in `users/api.py`

The `register` endpoint in `users/api.py:118` stores whatever string the client supplies in the `email` field, including an empty one, and writes it straight to the `users` table. The password-reset flow in `users/recovery.py:54` later reads that same column and has no address to send to, so the account is locked out of recovery for good.

```python
@app.post("/register")
def register():
    email = request.form["email"]
    User.create(email=email, password=hash(request.form["password"]))
```

Nothing else in the request path checks the value: the model schema in `users/models.py:24` declares `email = Column(String)` with no `not null` and no format constraint, and the form is the only entry point.

One guard before the call to `User.create` — `if not email or "@" not in email: abort(400)` — covers both the empty and the obviously-malformed case, and matches the style of the other field checks already in the same handler.
