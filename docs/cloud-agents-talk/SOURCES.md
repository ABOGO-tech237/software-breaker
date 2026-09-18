# Sources et journal d’inspection

Présentation du **samedi 19 septembre 2026**.  
Aucune capacité produit n’est inventée. Les cas s’appuient uniquement sur ce que cette VM a pu lire.

## Docs officielles Cursor (consultées le 18 sept. 2026)

| Sujet | URL |
| --- | --- |
| Cloud Agents (vue d’ensemble) | https://cursor.com/docs/cloud-agent.md |
| Capacités (Computer Use, artefacts, MCP, CI, abonnements) | https://cursor.com/docs/cloud-agent/capabilities.md |
| Aide Cloud Agents | https://cursor.com/help/ai-features/cloud-agents |
| Setup d’environnement | https://cursor.com/docs/cloud-agent/setup |
| Builds | https://cursor.com/docs/cloud-agent/builds.md |
| Sécurité | https://cursor.com/docs/cloud-agent/security |
| Réglages | https://cursor.com/docs/cloud-agent/settings |
| Worktrees (agents **locaux**) | https://cursor.com/docs/configuration/worktrees |
| CLI : handoff cloud (`&`) et `--worktree` | https://cursor.com/docs/cli/using |
| Computer Use (self-hosted) | https://cursor.com/docs/cloud-agent/bring-your-own-machine/computer-use |
| Agent local (outils, checkpoints) | https://cursor.com/docs/agent/overview |
| Blog Computer Use (24 fév. 2026) | https://cursor.com/blog/agent-computer-use |
| Page marketing Cloud | https://cursor.com/cloud |

`cursor-guide` n’est pas un outil disponible dans cette run. Les faits produit viennent des pages ci-dessus.

## Libellé « Try Live »

**Non vérifié** dans les docs officielles. Les docs parlent de **Computer use** et de **Remote desktop control** (prendre le contrôle du bureau de l’agent, puis le lui rendre).  
Ne pas présenter « Try Live » comme nom produit. Si l’UI affiche ce bouton le jour J, le décrire comme le contrôle du bureau distant documenté.

## Cette run Cloud Agent (preuve live)

| Champ | Valeur observée |
| --- | --- |
| URL | https://cursor.com/agents/bc-af5de014-b7c3-4e96-a308-ef22f425faf7 |
| Repo attaché | `github.com/abogo-tech237/software-breaker` |
| Workspace VM | `/workspace` (pas `/home/atangana/Projects/Cursor-Cameroun`) |
| Environnement | personnel, un seul repo, pas de `environment.json` exposé |
| Chemins frères | `/home/atangana/Projects` **absent** de cette VM |

## Repos demandés

| Projet | Cible demandée | Ce que cette VM a vu | 19 sept. 2026 |
| --- | --- | --- | --- |
| Cursor-Cameroun | https://github.com/Delmat237/Cursor-Cameroun.git | Clone public OK. Next.js 16.2.5, i18n FR/EN, events JSON, Drizzle. Site : https://cursor-cameroun-nine.vercel.app | Inspecté |
| software-breaker | https://github.com/ABOGO-tech237/software-breaker.git | Checkout local de **cette** run. Skill + subagent Full Chaos, README FR/EN | Inspecté |
| MobiYaounde / mobile_AI | `git@github.com:ABOGO-tech237/mobileAI.git` | `git ls-remote` + `gh repo view` : **Repository not found**. Absent de la liste publique `ABOGO-tech237`. Aucun checkout local | **Non inspecté** |
| EatNext | https://github.com/studio-crafiti/EatNext.git | Org/repo demandé : **404**. Clone public réussi : https://github.com/ABOGO-tech237/EatNext.git. Notion « EatNext : Rapport projet » (15 sept. 2026) | Inspecté via fork/public + Notion |
| Openspace | `git@github.com:ABOGO-tech237/openSpace.git` | **Repository not found**. Aucun checkout local | **Non inspecté** |
| crew | « seulement si inspectable localement » | Aucun dossier `crew` sous `/workspace`, `/home`, `/opt` | **Omis** — pas de remote inventé |

## Pages inspectées (extraits utiles)

### Cursor-Cameroun (`Delmat237/Cursor-Cameroun`, clone du 18 sept. 2026)

- README : site officiel communauté, Next.js 16.2.5, Tailwind 4, next-intl, Leaflet, Resend, charte N&B.
- Pages : Home, Events, Gallery, Roadmap, Community, contact, login, admin/events.
- `src/data/events.json` : plusieurs événements encore `upcoming` alors que la date du talk est le 19 sept. 2026 (ex. Café Douala 10 juin, Meetup Yaoundé 18 juillet).
- README marque encore « Carte 10 régions » et « migration WebP/AVIF » comme 🔄 ; `AGENT.md` les coche. À vérifier, pas à trancher sans Lighthouse.
- `src/data/roadmap.ts` : Yaoundé + Douala actives ; 8 villes `target` ; objectifs 2026 (2/6 villes, 3/18 événements, 180/1000 membres).

### software-breaker (checkout `/workspace`)

- Skill `.cusor/skills/software-breaker/` + agent `.cusor/agents/software-breaker.md` (typo dossier `.cusor` dans ce repo).
- Workflow Full Chaos : Scope → Map → Attack → Prove → Report → Improve.
- Guardrails : pas de fix auto sauf demande ; findings reproductibles ; pas de secrets dans les rapports.

### EatNext

- Repo public inspecté : `ABOGO-tech237/EatNext` (homepage GitHub `https://eat-next-three.vercel.app`).
- README repo : monorepo API Express/Prisma + frontend Vite/React, PostgreSQL, Redis, import Ayilaa ~1150 restos, OSM, branches `main` / `develop` / `feature/*`.
- Notion (15 sept. 2026) : découverte + avis, Crafti Studio, catalogue Ayilaa Yaoundé, Expo/RN + web Vercel, URLs `eatnext.vercel.app` / `eatnext-api.vercel.app`, repo cité `studio-crafiti/EatNext` (inaccessible ici).
- Ne pas inventer un résultat de test : cette VM n’a pas fait tourner l’app ni prouvé un bug.

## Outils contextuels

- Granola : MCP `needsAuth` — pas de notes de réunion.
- Notion : 1 page EatNext trouvée ; rien sur MobiYaounde / openSpace / ce talk.
- Slack ambassadeurs : rien de spécifique à ces repos (bruit « open space » = format d’événement).
