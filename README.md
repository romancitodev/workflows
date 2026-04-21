# Workflows

Mis workflows reutilizables para ahorrar tiempo en mis proyectos. Los mantengo centralizados para no copipastear el mismo código en cada repo.

## Rust

### Qué workflows hay

| Workflow | Qué hace |
|----------|----------|
| `ci` | Lint, tests y coverage |
| `lint` | Rustfmt y clippy |
| `release` | Publica en crates.io y crea release |
| `msrv` | Verifica MSRV |

### Setup básico

En `.github/workflows/ci.yml` de tu repo:

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  ci:
    uses: romancitodev/workflows/.github/workflows/rust-ci.yml@main
    secrets:
      CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }}
```

### Opciones útiles

**Modo estricto (no se puede mergear si fallan tests)**

```yaml
jobs:
  ci:
    uses: romancitodev/workflows/.github/workflows/rust-ci.yml@main
    with:
      strict-mode: true
    secrets:
      CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }}
```

**Flags para tests**

```yaml
with:
  cargo-test-flags: "--lib --doc"
```

**Flags para clippy**

```yaml
with:
  clippy-extra-flags: "-A clippy::too_many_arguments"
```

### Comandos en PRs

Puedes escribir en la descripción o en comentarios:

- `!execute` - Corre los tests
- `--skip-tests` - Se salta los tests

```
Este PR arregla el bug

!execute
```

O comentar directamente:

```
!execute --skip-tests
```

### Release

```yaml
name: Release

on:
  push:
    tags:
      - 'v*'

jobs:
  release:
    uses: romancitodev/workflows/.github/workflows/rust-release.yml@main
    secrets:
      CARGO_REGISTRY_TOKEN: ${{ secrets.CARGO_REGISTRY_TOKEN }}
```

Necesitas el token de crates.io y opcionalmente un `release.toml` si quieres configurar algo.
