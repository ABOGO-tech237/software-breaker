# Software Breaker for Cursor

**Full Chaos testing agent for Cursor IDE.**

Software Breaker pushes your code to its limits like a skilled adversary: edge cases, race conditions, auth gaps, error-path neglect, missing tests, and runtime failures. It produces **reproducible findings** and **concrete improvements** — not polite code review.

- **Skill + Subagent** — methodology + isolated deep-testing agent
- **Works in all projects** — install once in `~/.cursor/`
- **Bilingual reports** — FR or EN (severity labels in both languages)
- **Full Chaos by default** — runs tests, probes APIs, walks UI when env allows

---

## Table of contents

- [What's included](#whats-included)
- [Quick start](#quick-start)
- [Installation](#installation)
- [Usage](#usage)
- [Report format](#report-format)
- [Attack coverage](#attack-coverage)
- [Guardrails](#guardrails)
- [Troubleshooting](#troubleshooting)
- [Share with your team](#share-with-your-team)
- [Author](#author)
- [License](#license)

---

## What's included

```
.cursor/
├── skills/software-breaker/
│   ├── SKILL.md       # Methodology, Full Chaos workflow, report template
│   ├── reference.md   # Attack matrices (auth, concurrency, API, UI…)
│   ├── INSTALL.md     # Short install reference
│   └── README.md      # This file
└── agents/
    └── software-breaker.md   # Subagent system prompt
```

| Component | Role |
|-----------|------|
| **Skill** | Teaches Cursor the Full Chaos workflow, severity model, and report format |
| **Subagent** | Isolated agent persona for deep bug hunting sessions |

---

## Quick start

1. Install to `~/.cursor/` (see [Installation](#installation))
2. Open a **new Agent chat** in Cursor
3. Type:

```
/software-breaker on the auth module
```

or

```
teste à fond ce service avant release
```

---

## Installation

### Option A — Cursor prompt (recommended)

Open an **Agent chat** in Cursor and paste:

```
Installe Software Breaker dans mon environnement Cursor personnel.

Source : [URL_DU_REPO] (clone si nécessaire) ou le dossier ZIP déjà extrait.

Crée cette structure :
~/.cursor/skills/software-breaker/
  ├── SKILL.md
  ├── reference.md
  └── INSTALL.md
~/.cursor/agents/software-breaker.md

Étapes :
1. Clone le repo ou utilise le dossier local déjà présent
2. mkdir -p ~/.cursor/skills ~/.cursor/agents
3. Copie .cursor/skills/software-breaker/ vers ~/.cursor/skills/software-breaker/
4. Copie .cursor/agents/software-breaker.md vers ~/.cursor/agents/software-breaker.md
5. Vérifie que les 4 fichiers existent et affiche les chemins finaux

Ne modifie pas le contenu des fichiers. Ne commit rien sauf si je le demande.
```

**Repo déjà cloné localement** — prompt court :

```
Ce repo contient Software Breaker dans .cursor/. Installe-le dans mon Cursor personnel :

mkdir -p ~/.cursor/skills ~/.cursor/agents
cp -r .cursor/skills/software-breaker ~/.cursor/skills/
cp .cursor/agents/software-breaker.md ~/.cursor/agents/

Vérifie que SKILL.md, reference.md, INSTALL.md et software-breaker.md existent.
Dis-moi comment l'invoquer.
```

**Windows :** remplace `~/.cursor/` par `%USERPROFILE%\.cursor\`.

---

### Option B — Shell (Linux / macOS)

```bash
git clone [URL_DU_REPO] software-breaker
cd software-breaker

mkdir -p ~/.cursor/skills ~/.cursor/agents
cp -r .cursor/skills/software-breaker ~/.cursor/skills/
cp .cursor/agents/software-breaker.md ~/.cursor/agents/

# Verify
ls ~/.cursor/skills/software-breaker/
ls ~/.cursor/agents/software-breaker.md
```

---

### Option C — Shell (Windows PowerShell)

```powershell
git clone [URL_DU_REPO] software-breaker
cd software-breaker

New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.cursor\skills", "$env:USERPROFILE\.cursor\agents"
Copy-Item -Recurse .cursor\skills\software-breaker "$env:USERPROFILE\.cursor\skills\"
Copy-Item .cursor\agents\software-breaker.md "$env:USERPROFILE\.cursor\agents\"
```

---

### Option D — ZIP (sans git)

1. Télécharge : [URL_DU_ZIP]
2. Extrais l'archive
3. Copie manuellement :
   - dossier `software-breaker/` → `~/.cursor/skills/software-breaker/`
   - fichier `software-breaker.md` → `~/.cursor/agents/software-breaker.md`

Ou utilise l'**Option A** en indiquant le chemin du dossier extrait.

---

### Vérifier l'installation

Structure attendue :

```
~/.cursor/
├── skills/
│   └── software-breaker/
│       ├── SKILL.md
│       ├── reference.md
│       └── INSTALL.md
└── agents/
    └── software-breaker.md
```

Redémarre Cursor ou ouvre un **nouveau chat Agent** après installation.

---

## Usage

### Triggers

| Français | English |
|----------|---------|
| `teste à fond` | `stress test` |
| `casse ça` | `break it` |
| `chaos test` | `find bugs` |
| `trouve les bugs` | `pre-release review` |
| `/software-breaker` | `revue pré-release` |

### Exemples de prompts

**Module / feature :**

```
/software-breaker on the auth module
teste à fond le provisioning Docker
chaos test — find bugs in payment flow
```

**Pré-release :**

```
revue pré-release avec software-breaker
Use the software-breaker subagent for full pre-release review
```

**Stress API :**

```
casse ça — stress l'API login avec edge cases
break it — probe the spaces API for IDOR and race conditions
```

**Subagent (session profonde) :**

```
Use the software-breaker subagent on this repo — scope: branch changes, report in French
```

### Langue du rapport

FR ou EN selon ta langue. Labels de sévérité bilingues : `Critical / Critique`, `High / Élevé`, etc.

### Workflow Full Chaos

1. **Scope** — cible (module, diff, pré-release)
2. **Map** — surfaces d'attaque (routes, jobs, UI, cache, DB)
3. **Attack** — matrice d'attaque par priorité de risque
4. **Prove** — repro via tests, API, UI, logs
5. **Report** — tableau structuré des findings
6. **Improve** — tests manquants + durcissement

Pas de fix automatique sauf demande explicite.

---

## Report format

```markdown
# Rapport Software Breaker / Software Breaker Report

## Verdict
[1-2 phrases : risque global et readiness release]

## Findings (triés par sévérité / sorted by severity)

| Sévérité / Severity | Zone | Bug / faille / Finding | Preuve / repro / Proof | Impact |
|---------------------|------|------------------------|-------------------------|--------|

## Améliorations / Improvements

1. [Priority] Action concrète
2. ...

## Couverture / trous de tests / Test coverage gaps

- Missing: ...
- To add: ...

## Prochaines attaques suggérées / Suggested next attacks

- ...
```

### Niveaux de sévérité

| Niveau | Quand |
|--------|-------|
| **Critical / Critique** | Perte de données, bypass auth, RCE, breach, prod down |
| **High / Élevé** | Données incorrectes, escalade privilèges, crash loop |
| **Medium / Moyen** | Edge cases, erreurs faibles, chemins flaky |
| **Low / Faible** | UX mineure, cas rares |
| **Improvement / Amélioration** | Durcissement, couverture, observabilité |

Chaque finding inclut : **repro**, **expected vs actual**, **impact**.

---

## Attack coverage

| Catégorie | Exemples |
|-----------|----------|
| **Auth / sessions / JWT** | Auth manquante, expiry token, IDOR, rate limits |
| **Validation & injection** | Empty/null/max payloads, SQLi, XSS, path traversal |
| **Concurrency / races** | Double submit, TOCTOU, retries dupliqués |
| **Resource limits** | Timeouts, memory/CPU, goroutines illimitées |
| **API contract & errors** | Mauvais status codes, stack traces exposées |
| **UI / UX failure paths** | Double click, offline, session expirée |
| **Data integrity / multi-tenant** | Orphelins, isolation tenant, échecs partiels |

Probes adaptées Go/Fiber, JWT, PostgreSQL, Redis, Docker, Next.js si détectés.

---

## Guardrails

- Tests **défensifs** uniquement
- Pas d'attaque de systèmes tiers
- Pas de secrets / `.env` dans les rapports
- Findings **reproductibles** obligatoires
- **Pas de fix auto** sauf demande explicite
- Vulnérabilités **signalées**, pas weaponisées

---

## Troubleshooting

| Problème | Solution |
|----------|----------|
| L'agent ne réagit pas | Nouveau chat Agent + trigger `/software-breaker` |
| Skill introuvable | Vérifie `~/.cursor/skills/software-breaker/` |
| Un seul projet | Installe en **perso** `~/.cursor/`, pas seulement `.cursor/` projet |
| Windows | `%USERPROFILE%\.cursor\` au lieu de `~/.cursor/` |
| Subagent indispo | Mode inline Full Chaos via la skill |

---

## Share with your team

### Install perso (tous projets)

Copie vers `~/.cursor/` de chaque dev.

### Install projet (git)

Commit `.cursor/skills/software-breaker/` + `.cursor/agents/software-breaker.md`.

### ZIP communauté

Inclure :

- `.cursor/skills/software-breaker/` (SKILL.md, reference.md, INSTALL.md, README.md)
- `.cursor/agents/software-breaker.md`

Partager le **prompt Cursor** de l'[Option A](#option-a--cursor-prompt-recommended).

### Post Twitter / X

```
🧨 Software Breaker for Cursor — Full Chaos QA agent.
Skill + Subagent · FR/EN · reproducible bug reports + improvements.
Git: [URL_DU_REPO] · ZIP: [URL_DU_ZIP]
Triggers: /software-breaker · teste à fond · chaos test
```

---

## Author

**Emmanuel Atangana Abogo**  
Cursor Ambassador · AURORA IT Corporation

- Repository : [URL_DU_REPO]
- ZIP : [URL_DU_ZIP]

---

## License

MIT License

Copyright (c) 2026 Emmanuel Atangana Abogo

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
