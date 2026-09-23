# claude-plugins

Plugins de [Claude Code](https://claude.com/claude-code) reutilizables entre los repositorios del equipo.

## Plugins disponibles

### git-flow

Automatiza el flujo de git/GitHub (revisión de cambios, commit, push, creación de PR) adaptándose a la convención de cada repo. Ver [skills/git-flow/SKILL.md](skills/git-flow/SKILL.md).

## Instalación (una vez por persona)

El identificador interno de este marketplace es `atincopa-plugins` (no `claude-plugins`: ese nombre queda reservado para marketplaces oficiales de Anthropic). Úsalo tal cual en los comandos:

```bash
claude plugin marketplace add AlexanderTincopa/claude-plugins
claude plugin install git-flow@atincopa-plugins
```

O desde dentro de una sesión de Claude Code (CLI, no la extensión de VSCode — `/plugin` no está disponible ahí todavía):

```
/plugin marketplace add AlexanderTincopa/claude-plugins
/plugin install git-flow@atincopa-plugins
```

Verifica con `claude plugin list` que quedó `Status: enabled`. Una vez instalado (scope: user), la skill queda disponible en cualquier repo que abras en esa máquina, invocable como `/git-flow:git-flow` o simplemente pidiendo en lenguaje natural "sube estos cambios", "crea el PR", etc.

## Actualizar a la última versión

```bash
claude plugin update git-flow
```

## Agregar un plugin nuevo

Cada plugin vive en su propia carpeta en la raíz del repo, con su `skills/` y su propio registro en `.claude-plugin/marketplace.json`. Ver la [documentación oficial de plugins](https://code.claude.com/docs/en/plugins.md).
