# Workflows

Mis workflows reutilizables para automatizar tareas recurrentes en mis proyectos con GitHub Actions. Los mantengo centralizados acá para reutilizarlos fácilmente en otros repos.

## Rust

### Workflows disponibles

| Workflow | Descripción |
|----------|-------------|
| `ci` | Ejecuta las pruebas y valida el código |
| `lint` | Comprueba estilo y calidad del código |
| `build-report` | Compila el proyecto y genera un reporte de cobertura con Codecov |
| `release` | Automatiza el proceso de publicación y versionado |
| `msrv` | Verifica y registra la versión mínima soportada de Rust |

### Cómo usar

Referencia los workflows desde tus repos privados:

```yaml
jobs:
  my-job:
    uses: romancitodev/workflows/.github/workflows/rust/ci.yml@main
```
