# Software Breaker — Installation / Installation

## English

### What you get

- **Skill** — methodology, report format, Full Chaos workflow
- **Subagent** — isolated agent persona for deep bug hunting

### Install (personal — works in all projects)

```bash
# From a repo that contains .cursor/skills/software-breaker and .cursor/agents/software-breaker.md
mkdir -p ~/.cursor/skills ~/.cursor/agents
cp -r .cursor/skills/software-breaker ~/.cursor/skills/
cp .cursor/agents/software-breaker.md ~/.cursor/agents/
```

Or clone/copy the three skill files manually into `~/.cursor/skills/software-breaker/` and the agent file into `~/.cursor/agents/`.

### Install (project-only — share via git)

Commit these paths in your repository:

```
.cursor/skills/software-breaker/
.cursor/agents/software-breaker.md
```

Teammates copy to `~/.cursor/` as above, or rely on project-level agents/skills if their Cursor version loads `.cursor/` from the repo.

### Usage examples

```
/software-breaker on the auth module
teste à fond le provisioning Docker
chaos test — find bugs before release
Use the software-breaker subagent for pre-release review
casse ça — stress the login API
```

Reports follow FR or EN based on your message language.

---

## Français

### Contenu

- **Skill** — méthode, format de rapport, workflow Full Chaos
- **Subagent** — agent isolé pour chasse aux bugs en profondeur

### Installation (personnelle — tous les projets)

```bash
# Depuis un repo contenant .cursor/skills/software-breaker et .cursor/agents/software-breaker.md
mkdir -p ~/.cursor/skills ~/.cursor/agents
cp -r .cursor/skills/software-breaker ~/.cursor/skills/
cp .cursor/agents/software-breaker.md ~/.cursor/agents/
```

### Installation (projet — partage git)

Versionner dans le dépôt :

```
.cursor/skills/software-breaker/
.cursor/agents/software-breaker.md
```

Les collègues copient vers `~/.cursor/` ou utilisent la config projet selon leur Cursor.

### Exemples d'invocation

```
/software-breaker sur le module auth
teste à fond le provisioning Docker
chaos test — trouve les bugs avant release
revue pré-release avec software-breaker
casse ça — stress l'API login
```

Les rapports sont en FR ou EN selon la langue de votre message.

---

## Ambassador sharing

Package for workshops:

1. Zip `.cursor/skills/software-breaker/` + `.cursor/agents/software-breaker.md`
2. Share `INSTALL.md` with copy commands
3. Demo triggers: `/software-breaker`, `teste à fond`, `chaos test`

**Guardrails to mention:** defensive testing only; reproducible findings; no auto-fix unless requested.
