# git-worktrees

> Dos agentes, dos carpetas, cero archivos pisados.

**Trabajo en paralelo con git worktrees** · Skill para agentes de código de la comunidad [nvvdev](https://github.com/nvv-dev). Funciona en Claude Code como plugin o como skill suelta, y en cualquier agente compatible con el formato abierto [`SKILL.md`](https://agentskills.io).

*English summary at the end.*

## Qué hace

Crea un worktree por tarea en su propia rama, explica cómo trabajar sin tocar los de otros y cómo limpiarlos de forma segura, sin forzar borrados que pierden trabajo.

## Objetivo

Poder correr varios agentes sobre el mismo repo al mismo tiempo sin conflictos.

## Cuándo usarla

- Varios agentes o tú y un agente trabajan en el mismo repo
- Empezar una tarea aislada sin tocar tu checkout actual

## Cuándo no

- Un solo flujo de trabajo secuencial

## Ejemplo

```text
Prepara un worktree para la tarea fix/login-timeout.
```

## Cómo se activa

Esta skill **se activa sola**: Claude Code lee su descripción y la carga cuando la tarea coincide. También puedes pedirla por nombre ("usa la skill git-worktrees") o invocarla con `/git-worktrees:git-worktrees` (plugin) o `/git-worktrees` (copiada a `.claude/skills/`).

## Instalación

### Opción 1: Claude Code, como plugin (recomendada)

Dentro de Claude Code:

```text
/plugin marketplace add nvv-dev/claude-plugins
/plugin install git-worktrees@nvvdev
```

La primera línea agrega el catálogo de nvvdev una sola vez; la segunda instala esta skill. Si prefieres el paquete completo, instala `dev-workflow@nvvdev` en su lugar (incluye esta skill y las demás de [dev-workflow](https://github.com/nvv-dev/dev-workflow)); no instales los dos a la vez.

### Opción 2: Claude Code, copiando la skill

Para un solo proyecto (se comparte con tu equipo por git):

```bash
git clone --depth 1 https://github.com/nvv-dev/git-worktrees.git /tmp/git-worktrees
mkdir -p .claude/skills
cp -R /tmp/git-worktrees/skills/git-worktrees .claude/skills/
```

Para todos tus proyectos, cópiala en `~/.claude/skills/` en lugar de `.claude/skills/`.

### Opción 3: otros agentes

Copia la carpeta `skills/git-worktrees/` en la carpeta de skills de tu agente (cada agente documenta la suya). Con la CLI [skills](https://github.com/vercel-labs/skills) de Vercel Labs:

```bash
DISABLE_TELEMETRY=1 npx skills add nvv-dev/git-worktrees
```

### Verificar

Abre una sesión nueva y pregunta "¿qué skills tienes disponibles?"; `git-worktrees` debe aparecer. Con el plugin, `/plugin` la muestra como instalada.

### Actualizar o desinstalar

- Plugin: `/plugin marketplace update nvvdev` para actualizar; `/plugin uninstall git-worktrees@nvvdev` para quitarla.
- Copia manual: repite la copia para actualizar, o borra la carpeta `.claude/skills/git-worktrees`.

Antes de instalar cualquier skill, incluida esta, conviene leerla: es un solo archivo, [`skills/git-worktrees/SKILL.md`](skills/git-worktrees/SKILL.md). Ver [vetting-external-skills](https://github.com/nvv-dev/vetting-external-skills).

## Contenido

| Ruta | Qué es |
|---|---|
| `skills/git-worktrees/SKILL.md` | La skill: instrucciones en inglés para que los escáneres de seguridad las analicen completas; el agente responde en tu idioma |
| `.claude-plugin/plugin.json` | Manifiesto para instalarla como plugin |
| `.github/workflows/` | Validación de estructura y escaneo con SkillSpector en cada cambio |

## Contribuir

Este repo se **genera** desde [nvv-dev/dev-workflow](https://github.com/nvv-dev/dev-workflow), donde vive la versión canónica. Abre issues y PRs allí. La mejor contribución es un caso real en la sección *Known failures* de la skill, con la regla que lo evita.

## Origen

Escrita desde cero por nvvdev. Inspirada en: [obra/superpowers](https://github.com/obra/superpowers) (using-git-worktrees).

## Licencia

MIT.

---

## English

**git-worktrees** — One worktree per task on its own branch, with safe cleanup that never discards work.

Install in Claude Code with `/plugin marketplace add nvv-dev/claude-plugins` and `/plugin install git-worktrees@nvvdev`, or copy `skills/git-worktrees/` into `.claude/skills/` (project) or `~/.claude/skills/` (personal). Other agents: copy the folder into their skills directory, or run `DISABLE_TELEMETRY=1 npx skills add nvv-dev/git-worktrees`. Loads automatically when the task matches its description. Canonical source: [nvv-dev/dev-workflow](https://github.com/nvv-dev/dev-workflow). License: MIT.
