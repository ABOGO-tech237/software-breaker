# Cloud Agents, sur nos projets

Cursor Cameroun · samedi 19 septembre 2026 · 15–20 min

Ouvrir de préférence [index.html](index.html). Ce fichier est la version Markdown imprimable.

---

## Pourquoi ce talk

L’agent local suffit… jusqu’au plafond du laptop. Le cloud : une VM par tâche, parallèle, laptop optionnel.

## Définition

Mêmes fondamentaux d’agent, VM Ubuntu isolée. Builder, tester, cliquer l’UI. MCP. Multi-repos (pas de long-running encore). Ancien nom : Background Agents.

## Cloud vs local

| Local | Cloud |
| --- | --- |
| Ton checkout / worktree | Clone Git distant, branche neuve |
| Checkpoints locaux | PR draft + artefacts |
| `~/.cursor` hooks/skills | Skills repo ; Sync Skills pour le perso |
| Laptop occupé | Laptop optionnel |

« Move to Cloud » ne prend **pas** les fichiers non commités.

## Boucle

Start → VM Firecracker → clone → branche séparée → PR draft (commits Verified). Rien ne merge tout seul.

## Lancer

Desktop Cloud · cursor.com/agents · iOS · Slack/Linear `@cursor` · GitHub `@cursor` · CLI `&` · API · Automations. Plan payant + SCM.

## Computer Use

Souris, clavier, navigateur. Artefacts. Remote desktop control. **« Try Live » non trouvé dans les docs.**

## Usages / limites

Usages : feature/bug/tests hors ligne, parallèle, multi-repos, kickoff Slack/GitHub, auto-CI Teams+GHA sur PR agent.

Limites : env à préparer, pas de dirty local, pas de hooks home, pièces jointes web 4/15 Mo, egress, revue humaine. Cette VM ne voyait pas `/home/atangana/Projects`.

## Cas

1. **Cursor-Cameroun** (inspecté) — ajouter l’event du 19 sept., corriger les `upcoming` périmés, vérifier FR/EN.
2. **software-breaker** (inspecté ici) — rapport Full Chaos, pas de fix auto. Ce deck = cette run.
3. **mobileAI** — remote 404, pas de stack inventée.
4. **EatNext** — public `ABOGO-tech237/EatNext` ; `studio-crafiti` 404. Env DB + flux avis, PR `develop`. App non exécutée ici.
5. **openSpace** — remote 404.
6. **crew** — pas local, omis.

## Live

1. Lancer un Cloud Agent (prompt dans README).
2. Montrer cette run / PR.
3. Bureau distant sur cursor-cameroun-nine.vercel.app.

## Close

Local pour itérer. Cloud pour isoler et prouver. Sources : [SOURCES.md](SOURCES.md).
