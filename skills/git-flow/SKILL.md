---
name: git-flow
description: Automatiza el flujo de git/GitHub (revision de cambios, commit, push y creacion de PR) adaptandose a la convencion de nomenclatura de cada repo. Usar cuando el usuario pida "haz un commit", "sube estos cambios", "crea el PR", "revisa mis cambios antes de subir" o equivalentes.
---

# Git flow del equipo

Skill generica y portable: sirve en cualquier repositorio, no asume una convencion de nombres fija. Antes de proponer nombres de rama o mensajes de commit, identifica la convencion real del proyecto donde te encuentras.

## Paso 0: identifica la convencion del repo

En este orden, hasta encontrar señal:

1. Busca `CONTRIBUTING.md` o una seccion de "Flujo de contribucion" / "Contributing" en el README.
2. Si no hay documentacion, mira `git log --oneline -20` y `git branch -a` para inferir el patron real que ya usa el equipo (formato de rama, si usan Conventional Commits o mensajes libres).
3. Si tampoco hay señal clara (repo nuevo, sin historial), pregunta al usuario que convencion prefiere antes de continuar.

Si el repo tiene hooks de git (Husky, commitlint, pre-commit/pre-push) que ya validan formato, o una skill de proyecto con detalles especificos de ese repo, respetalos como fuente de verdad — no los reemplaces, combinalos con estos pasos.

## Pasos

1. **Diagnostico**: `git status` + `git diff` (staged y unstaged). Avisa si hay archivos que no deberian ir (secretos, artifacts generados, dependencias, credenciales, reportes/videos de pruebas).
2. **Revision de contenido**: lee el diff real, no solo los nombres de archivo. Señala codigo de depuracion olvidado (`console.log`, `print`, `debugger`), tests deshabilitados (`.only`/`.skip`), cambios sin relacion mezclados entre si, posibles secretos o tokens.
3. **Verifica la rama**: si estas en la rama principal (`master`/`main`) o el nombre no sigue la convencion identificada en el Paso 0, crea una rama nueva antes de commitear.
4. **Staging selectivo**: `git add <archivos>` explicitos, nunca `git add -A`/`git add .` a ciegas. Confirma con el usuario que se va a incluir si hay dudas.
5. **Mensaje de commit**: redactalo siguiendo la convencion identificada, basado en el diff real (no en lo que el usuario dijo de forma informal). Preséntaselo antes de commitear.
6. **Commit**: ejecuta el commit. Si un hook lo rechaza, corrige el mensaje y reintenta — nunca uses `--no-verify` para saltarte la validacion.
7. **Push**: pide confirmacion antes de este paso si no fue pedido explicitamente junto con el commit.
8. **Pull request**: si el proyecto usa GitHub y `gh` esta instalado y autenticado, usa `gh pr create` con un body que incluya `## Summary` y `## Test plan`. Si `gh` no esta autenticado, avisa y pide al usuario correr `gh auth login` el mismo (es un flujo interactivo que no se puede automatizar).
9. **Despues del merge** (solo cuando el usuario confirme que ya se mergeo, nunca antes): sincroniza la rama principal local (`checkout` + `pull --ff-only`) y borra la rama local ya integrada.

## Limites explicitos

- No hagas `git push --force` salvo pedido explicito.
- No hagas merge de un PR salvo pedido explicito del usuario — el merge siempre depende de un revisor humano.
- No uses `--no-verify` para saltarte hooks; si un hook falla, el fix es corregir el commit, no saltarselo.
- No asumas una convencion de nomenclatura sin antes intentar identificarla (Paso 0).
