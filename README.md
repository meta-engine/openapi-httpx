# MetaEngine OpenAPI Python FastAPI

[![PyPI version](https://img.shields.io/pypi/v/metaengine-openapi-fastapi.svg)](https://pypi.org/project/metaengine-openapi-fastapi/)
[![Python versions](https://img.shields.io/pypi/pyversions/metaengine-openapi-fastapi.svg)](https://pypi.org/project/metaengine-openapi-fastapi/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**Generate idiomatic Python clients and models from OpenAPI/Swagger specifications.**

Pydantic v2 models and an async `httpx` client — typed, with optional docstrings, validation, and camelCase field aliases.

> **No .NET required.** Unlike most MetaEngine wrappers, each wheel bundles a **self-contained, platform-native binary** — `pip install` and run. There is nothing else to install.

---

## Quick Links

- **PyPI Package**: [metaengine-openapi-fastapi](https://pypi.org/project/metaengine-openapi-fastapi/)
- **NuGet Package**: [MetaEngine.Python.OpenApi.FastApi](https://www.nuget.org/packages/MetaEngine.Python.OpenApi.FastApi)
- **Website**: [metaengine.eu](https://www.metaengine.eu)

---

## Features

- ✅ **Self-contained** - Bundled native binary per platform; no .NET runtime to install
- ✅ **Pydantic v2 models** - `BaseModel` with `ConfigDict`, typed fields, required vs optional
- ✅ **Async httpx client** - One service class per OpenAPI tag, `model_validate` on responses
- ✅ **camelCase aliases** - snake_case Python properties mapped to camelCase wire names via `Field(alias=...)`
- ✅ **Enums** - Standalone Python enum types, properly serialized
- ✅ **Docstrings** - Optional doc-comment generation from OpenAPI descriptions and examples
- ✅ **Tag Filtering** - Generate only the operations you need
- ✅ **Options Object** - Collapse long parameter lists into an options object past a threshold

---

## Installation

```bash
pip install metaengine-openapi-fastapi
```

Pre-built wheels are published for Linux (x86_64, aarch64), macOS (Apple Silicon + Intel), and Windows (x64).

---

## Requirements

- **Python 3.8** or later
- **No .NET runtime** - the wheel ships a self-contained native binary for your platform

---

## Quick Start

```bash
metaengine-openapi-fastapi <input> <output> [options]
```

### Recommended Setup

```bash
metaengine-openapi-fastapi api.yaml ./generated \
  --camel-case-aliases \
  --documentation
```

### More Examples

```bash
# From a URL
metaengine-openapi-fastapi https://api.example.com/openapi.json ./generated

# Filter by OpenAPI tags
metaengine-openapi-fastapi api.yaml ./generated --include-tags orders,users

# Strict spec validation + verbose logging
metaengine-openapi-fastapi api.yaml ./generated --strict-validation --verbose
```

---

## CLI Options

| Argument / Option | Description | Default |
|---|---|---|
| `input` *(required)* | OpenAPI specification file path or URL | - |
| `output` *(required)* | Output directory for generated Python files | - |
| `--include-tags <tags>` | Only generate operations with these tags (comma-separated) | - |
| `--service-suffix <name>` | Service class naming suffix | `Service` |
| `--options-threshold <n>` | Parameter count at which a method switches to an options object | `4` |
| `--camel-case-aliases` | Generate camelCase field aliases for Pydantic models | `false` |
| `--documentation` | Generate docstring comments | `false` |
| `--strict-validation` | Enable strict OpenAPI validation | `false` |
| `--verbose` | Enable verbose logging | `false` |

---

## Generated Code Structure

```
output/
  ├── models/                    # One file per schema (Pydantic v2)
  │   ├── order.py               # class Order(BaseModel): ...
  │   ├── order_status.py        # standalone enum type
  │   └── ...
  └── services/                  # One async httpx client per tag
      ├── orders_service.py      # class OrdersService with all order operations
      └── ...
```

Models use Pydantic v2 (`BaseModel` + `ConfigDict`); with `--camel-case-aliases`, snake_case
properties carry a `Field(alias=...)` mapping to the wire name and `populate_by_name=True`:

```python
class Order(BaseModel):
    model_config = ConfigDict(populate_by_name=True)
    id: int
    customer_name: str = Field(alias='customerName')
    total_amount: float | None = Field(default=None, alias='totalAmount')
```

---

## Support

- **Issues**: [GitHub Issues](https://github.com/meta-engine/openapi-fastapi/issues)
- **Email**: info@metaengine.eu
- **Website**: [metaengine.eu](https://www.metaengine.eu)

---

## License

MIT License - see [LICENSE](./LICENSE) file for details.

---

## About This Repository

This is the **documentation and issue tracking repository** for MetaEngine OpenAPI Python FastAPI. The package is published to [PyPI](https://pypi.org/project/metaengine-openapi-fastapi/).

Source code is proprietary, but the package is free to use under the MIT license.
