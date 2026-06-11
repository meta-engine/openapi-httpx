# Changelog

See the [PyPI releases page](https://pypi.org/project/metaengine-openapi-fastapi/#history) for the full version history.

## 1.0.0

- Initial release — Python code generation from OpenAPI specifications
- **Pydantic v2 models** — `BaseModel` with `ConfigDict`, typed required/optional fields, standalone enum types
- **Async httpx client** — one service class per OpenAPI tag
- `--camel-case-aliases` — snake_case properties with `Field(alias=...)` camelCase wire mapping
- `--documentation` — docstring generation from OpenAPI descriptions and examples
- `--include-tags`, `--service-suffix`, `--options-threshold`, `--strict-validation`, `--verbose`
- **Self-contained** — each platform wheel bundles a native binary; no .NET runtime required
