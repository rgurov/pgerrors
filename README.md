# PGErrors

Simple Go library with all PostgreSQL error codes
See: https://www.postgresql.org/docs/current/errcodes-appendix.html

Example of using Is method

```go
func CreateUser(ctx context.Context, email, password string) (int, error) {
    sql = `insert into users (email, password) value ($1, $2) returning id`
    var id int
    err := client.QueryRow(ctx, sql, email, password).Scan(&id)
    if err != nil {
        if pgerrors.Is(err, pgerrors.UniqueViolation) {
            return 0, errors.New("email is busy")
        }
        return 0, err
    }
    return id, nil
}
```
