# claude-plugins

Plugins de [Claude Code](https://claude.com/claude-code) reutilizables entre los repositorios del equipo.

## Plugins disponibles

### git-flow

Automatiza el flujo de git/GitHub (revisión de cambios, commit, push, creación de PR) adaptándose a la convención de cada repo. Ver [skills/git-flow/SKILL.md](skills/git-flow/SKILL.md).

## Instalación (una vez por persona)

```bash
claude plugin marketplace add AlexanderTincopa/claude-plugins
claude plugin install git-flow@claude-plugins
```

O desde dentro de una sesión de Claude Code:

```
/plugin marketplace add AlexanderTincopa/claude-plugins
/plugin install git-flow@claude-plugins
```

Una vez instalado, la skill queda disponible en cualquier repo que abras, invocable como `/git-flow:git-flow` o simplemente pidiendo en lenguaje natural "sube estos cambios", "crea el PR", etc.

## Actualizar a la última versión

```
/plugin marketplace update claude-plugins
```

## Agregar un plugin nuevo

Cada plugin vive en su propia carpeta en la raíz del repo, con su `skills/` y su propio registro en `.claude-plugin/marketplace.json`. Ver la [documentación oficial de plugins](https://code.claude.com/docs/en/plugins.md).
