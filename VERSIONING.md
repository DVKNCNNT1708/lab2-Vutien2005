# VERSIONING

This project follows semantic versioning principles and documents versioning decisions for API evolution.

## Versioning policy

- Use `MAJOR.MINOR.PATCH` versioning.
- `MAJOR` increment for breaking changes.
- `MINOR` increment for backward-compatible feature additions.
- `PATCH` increment for bug fixes and non-breaking maintenance.
- Deprecated endpoints or schema fields must be marked with `deprecated: true` in `openapi.yaml`.
- Deprecated resources must also include a `Sunset` response header to inform clients of planned removal.

## Backward-compatible change

A backward-compatible change preserves all existing clients while adding new functionality.

Example:

- Add cursor-based pagination support for list endpoints without changing existing query parameters for current clients.
- Add an optional `filter` or `sort` query parameter to an existing GET endpoint.

This type of change should increment the `MINOR` version.

## Breaking change

A breaking change modifies the API in a way that existing clients may fail unless they update.

Example:

- Remove or rename an existing required response field.
- Change the data type of a returned property from integer to string.
- Remove an endpoint or change its path.

This type of change requires a `MAJOR` version increment.

## Deprecation and Sunset

When an endpoint or field is no longer recommended, mark it as deprecated and provide a Sunset date.

Example API annotation in `openapi.yaml`:

```yaml
paths:
  /old-resource:
    get:
      deprecated: true
      responses:
        '200':
          description: OK
      headers:
        Sunset:
          description: Date after which this resource will be removed
          schema:
            type: string
```

Example Sunset header:

```
Sunset: Wed, 31 Dec 2025 23:59:59 GMT
```

## Versioning summary

- Backward-compatible changes: `MINOR` update.
- Bug fixes/non-breaking updates: `PATCH` update.
- Breaking changes: `MAJOR` update.
- Deprecated features: use `deprecated: true` and `Sunset` header.
